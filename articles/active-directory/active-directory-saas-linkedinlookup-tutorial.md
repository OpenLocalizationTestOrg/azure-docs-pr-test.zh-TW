---
title: "教學課程：Azure Active Directory 與 LinkedIn Lookup 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 LinkedIn 查閱之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="cac91-103">教學課程：Azure Active Directory 與 LinkedIn Lookup 整合</span><span class="sxs-lookup"><span data-stu-id="cac91-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="cac91-104">在此教學課程中，您學會如何 toointegrate LinkedIn 查閱與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="cac91-104">In this tutorial, you learn how toointegrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cac91-105">與 Azure AD 整合 LinkedIn 查閱可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="cac91-105">Integrating LinkedIn Lookup with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cac91-106">您可以控制存取 tooLinkedIn 查閱 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="cac91-106">You can control in Azure AD who has access tooLinkedIn Lookup</span></span>
- <span data-ttu-id="cac91-107">您可以啟用您的使用者 tooautomatically get 登入 tooLinkedIn （單一登入） 查閱使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="cac91-107">You can enable your users tooautomatically get signed-on tooLinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cac91-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cac91-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cac91-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cac91-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cac91-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cac91-110">Prerequisites</span></span>

<span data-ttu-id="cac91-111">tooconfigure LinkedIn 查閱與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="cac91-111">tooconfigure Azure AD integration with LinkedIn Lookup, you need hello following items:</span></span>

- <span data-ttu-id="cac91-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cac91-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cac91-113">已啟用 LinkedIn Lookup 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cac91-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cac91-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="cac91-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cac91-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="cac91-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cac91-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cac91-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cac91-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="cac91-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cac91-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="cac91-118">Scenario description</span></span>
<span data-ttu-id="cac91-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cac91-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cac91-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="cac91-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cac91-121">從 hello 圖庫加入 LinkedIn 查閱</span><span class="sxs-lookup"><span data-stu-id="cac91-121">Adding LinkedIn Lookup from hello gallery</span></span>
2. <span data-ttu-id="cac91-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cac91-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-hello-gallery"></a><span data-ttu-id="cac91-123">從 hello 圖庫加入 LinkedIn 查閱</span><span class="sxs-lookup"><span data-stu-id="cac91-123">Adding LinkedIn Lookup from hello gallery</span></span>
<span data-ttu-id="cac91-124">tooconfigure hello 整合 LinkedIn 查閱到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd LinkedIn 查閱。</span><span class="sxs-lookup"><span data-stu-id="cac91-124">tooconfigure hello integration of LinkedIn Lookup into Azure AD, you need tooadd LinkedIn Lookup from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cac91-125">**tooadd LinkedIn 查閱，從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cac91-125">**tooadd LinkedIn Lookup from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cac91-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cac91-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cac91-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cac91-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cac91-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cac91-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="cac91-131">按一下**新的應用程式**上 hello hello 對話方塊 tooadd 新應用程式頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="cac91-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="cac91-133">在 [hello] 搜尋方塊中，輸入**LinkedIn 查閱**。</span><span class="sxs-lookup"><span data-stu-id="cac91-133">In hello search box, type **LinkedIn Lookup**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="cac91-135">在 hello 結果 窗格中，選取  **LinkedIn 查閱**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cac91-135">In hello results panel, select **LinkedIn Lookup**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cac91-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cac91-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cac91-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 LinkedIn Lookup 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cac91-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cac91-139">單一登入 toowork，Azure AD 需要 tooknow LinkedIn 查閱中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="cac91-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Lookup is tooa user in Azure AD.</span></span> <span data-ttu-id="cac91-140">換句話說，Azure AD 使用者和 LinkedIn 查閱中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="cac91-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Lookup needs toobe established.</span></span>

<span data-ttu-id="cac91-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** LinkedIn 查閱中。</span><span class="sxs-lookup"><span data-stu-id="cac91-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="cac91-142">tooconfigure 及 LinkedIn 查閱與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="cac91-142">tooconfigure and test Azure AD single sign-on with LinkedIn Lookup, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cac91-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="cac91-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cac91-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="cac91-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cac91-145">**[建立測試使用者 LinkedIn 查閱](#creating-an-linkedin-lookup-test-user)** -toohave 許 Simon LinkedIn 查閱所連結的 toohello Azure AD 的表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="cac91-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Lookup that is linked toohello Azure AD representation.</span></span>
4. <span data-ttu-id="cac91-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cac91-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cac91-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="cac91-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cac91-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cac91-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cac91-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 LinkedIn 查閱應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="cac91-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="cac91-150">**tooconfigure Azure AD 單一登入搭配 LinkedIn 查閱，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cac91-150">**tooconfigure Azure AD single sign-on with LinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="cac91-151">在 Azure 入口網站上 hello hello **LinkedIn 查閱**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="cac91-151">In hello Azure portal, on hello **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="cac91-153">在 hello**單一登入**對話方塊，請在**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cac91-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="cac91-155">在不同的網頁瀏覽器視窗中，登入 tooyour **LinkedIn 查閱**身為系統管理員的網站。</span><span class="sxs-lookup"><span data-stu-id="cac91-155">In a different web browser window, sign-on tooyour **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="cac91-156">在 [帳戶中心] 中，按一下 [設定] 底下的 [全域設定]。</span><span class="sxs-lookup"><span data-stu-id="cac91-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="cac91-157">此外，選取**查閱**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="cac91-157">Also, select **Lookup** from hello dropdown list.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="cac91-159">按一下**或按一下這裡 tooload 並複製個別欄位從 hello 表單**和複製**實體識別碼**和**判斷提示取用者存取 (ACS) Url**</span><span class="sxs-lookup"><span data-stu-id="cac91-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="cac91-161">在 Azure 入口網站，在**LinkedIn 查閱網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="cac91-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="cac91-163">a.</span><span class="sxs-lookup"><span data-stu-id="cac91-163">a.</span></span> <span data-ttu-id="cac91-164">在 hello**識別碼**文字方塊中，輸入 hello**實體識別碼**從 LinkedIn 入口網站複製</span><span class="sxs-lookup"><span data-stu-id="cac91-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="cac91-165">b.</span><span class="sxs-lookup"><span data-stu-id="cac91-165">b.</span></span> <span data-ttu-id="cac91-166">在 hello**回覆 URL**文字方塊中，輸入 hello**判斷提示取用者存取 (ACS) Url**從 LinkedIn 入口網站複製</span><span class="sxs-lookup"><span data-stu-id="cac91-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="cac91-167">請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="cac91-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="cac91-169">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="cac91-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="cac91-170">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="cac91-170">This is not real value.</span></span> <span data-ttu-id="cac91-171">hello 使用者具有 tooupdate 這些值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="cac91-171">hello user has tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="cac91-172">請連絡[LinkedIn 查閱用戶端支援小組](https://business.LinkedIn.com/lookup)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="cac91-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) tooget this value.</span></span>

8. <span data-ttu-id="cac91-173">您**LinkedIn 查閱**應用程式特定的格式預期 hello SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="cac91-173">Your **LinkedIn Lookup** application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="cac91-174">hello 使用者具有 tooadd 自訂屬性對應 toohello SAML 權杖屬性的組態。</span><span class="sxs-lookup"><span data-stu-id="cac91-174">hello user has tooadd custom attribute mappings toohello SAML token attributes configuration.</span></span> <span data-ttu-id="cac91-175">下列螢幕擷取畫面的 hello 顯示範例。</span><span class="sxs-lookup"><span data-stu-id="cac91-175">hello following screenshot shows an example.</span></span> <span data-ttu-id="cac91-176">hello 預設值是**使用者識別碼**是**user.userprincipalname**但 LinkedIn 查閱預期這個 toobe hello 使用者的電子郵件地址的對應。</span><span class="sxs-lookup"><span data-stu-id="cac91-176">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="cac91-177">您可以使用**user.mail**屬性從 hello 清單或使用您組織的組態為基礎的 hello 適當的屬性值。</span><span class="sxs-lookup"><span data-stu-id="cac91-177">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="cac91-179">在**使用者屬性**區段中，按一下**檢視和編輯所有其他使用者屬性**，並設定 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="cac91-179">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="cac91-180">hello 使用者需要 tooadd 四個宣告名為**電子郵件**，**部門**， **firstname**，和**lastname** hello 值是使用對應的 toobe**user.mail**， **user.department**， **user.givenname**，和**user.surname**分別</span><span class="sxs-lookup"><span data-stu-id="cac91-180">hello user needs tooadd four claims named **email**,  **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="cac91-181">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="cac91-181">Attribute Name</span></span> | <span data-ttu-id="cac91-182">屬性值</span><span class="sxs-lookup"><span data-stu-id="cac91-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="cac91-183">電子郵件</span><span class="sxs-lookup"><span data-stu-id="cac91-183">email</span></span>| <span data-ttu-id="cac91-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="cac91-184">user.mail</span></span> |    
    | <span data-ttu-id="cac91-185">department</span><span class="sxs-lookup"><span data-stu-id="cac91-185">department</span></span>| <span data-ttu-id="cac91-186">user.department</span><span class="sxs-lookup"><span data-stu-id="cac91-186">user.department</span></span> |
    | <span data-ttu-id="cac91-187">firstname</span><span class="sxs-lookup"><span data-stu-id="cac91-187">firstname</span></span>| <span data-ttu-id="cac91-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="cac91-188">user.givenname</span></span> |
    | <span data-ttu-id="cac91-189">lastname</span><span class="sxs-lookup"><span data-stu-id="cac91-189">lastname</span></span>| <span data-ttu-id="cac91-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="cac91-190">user.surname</span></span> |

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="cac91-192">a.</span><span class="sxs-lookup"><span data-stu-id="cac91-192">a.</span></span> <span data-ttu-id="cac91-193">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cac91-193">Click **Add Attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="cac91-196">b.</span><span class="sxs-lookup"><span data-stu-id="cac91-196">b.</span></span> <span data-ttu-id="cac91-197">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="cac91-197">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="cac91-198">c.</span><span class="sxs-lookup"><span data-stu-id="cac91-198">c.</span></span> <span data-ttu-id="cac91-199">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="cac91-199">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="cac91-200">d.</span><span class="sxs-lookup"><span data-stu-id="cac91-200">d.</span></span> <span data-ttu-id="cac91-201">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="cac91-201">Click **Ok**</span></span>

10. <span data-ttu-id="cac91-202">執行下列步驟在 hello hello**名稱**屬性-</span><span class="sxs-lookup"><span data-stu-id="cac91-202">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="cac91-203">a.</span><span class="sxs-lookup"><span data-stu-id="cac91-203">a.</span></span> <span data-ttu-id="cac91-204">按一下 hello 屬性 tooopen hello**編輯屬性**視窗。</span><span class="sxs-lookup"><span data-stu-id="cac91-204">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="cac91-206">b.</span><span class="sxs-lookup"><span data-stu-id="cac91-206">b.</span></span> <span data-ttu-id="cac91-207">從 hello 刪除 hello URL 值**命名空間**。</span><span class="sxs-lookup"><span data-stu-id="cac91-207">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="cac91-208">c.</span><span class="sxs-lookup"><span data-stu-id="cac91-208">c.</span></span> <span data-ttu-id="cac91-209">按一下**確定**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="cac91-209">Click **Ok** toosave hello setting.</span></span>

10. <span data-ttu-id="cac91-210">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="cac91-210">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="cac91-212">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="cac91-212">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="cac91-214">跳過**LinkedIn 的管理設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="cac91-214">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="cac91-215">上傳 hello XML 檔案從 hello Azure 入口網站下載按一下 hello**上載 XML 檔案**選項。</span><span class="sxs-lookup"><span data-stu-id="cac91-215">Upload hello XML file you downloaded from hello Azure portal by clicking hello **Upload XML file** option.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="cac91-217">按一下**上**tooenable SSO。</span><span class="sxs-lookup"><span data-stu-id="cac91-217">Click **On** tooenable SSO.</span></span> <span data-ttu-id="cac91-218">SSO 狀態變更從**未連接**太**已連線**</span><span class="sxs-lookup"><span data-stu-id="cac91-218">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="cac91-220">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="cac91-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cac91-221">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="cac91-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cac91-222">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cac91-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cac91-223">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cac91-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="cac91-224">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="cac91-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="cac91-226">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cac91-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cac91-227">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cac91-227">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cac91-229">跳過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="cac91-229">Go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cac91-231">按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cac91-231">Click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cac91-233">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cac91-233">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cac91-235">a.</span><span class="sxs-lookup"><span data-stu-id="cac91-235">a.</span></span> <span data-ttu-id="cac91-236">在 hello**名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="cac91-236">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="cac91-237">b.</span><span class="sxs-lookup"><span data-stu-id="cac91-237">b.</span></span> <span data-ttu-id="cac91-238">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**許 Simon。</span><span class="sxs-lookup"><span data-stu-id="cac91-238">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="cac91-239">c.</span><span class="sxs-lookup"><span data-stu-id="cac91-239">c.</span></span> <span data-ttu-id="cac91-240">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="cac91-240">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cac91-241">d.</span><span class="sxs-lookup"><span data-stu-id="cac91-241">d.</span></span> <span data-ttu-id="cac91-242">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cac91-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="cac91-243">建立 LinkedIn Lookup 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cac91-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="cac91-244">連結的查閱應用程式支援恰好在 Time (JIT) 使用者佈建，以及之後驗證使用者會自動建立 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="cac91-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="cac91-245">啟動**自動指派授權**tooassign 授權 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="cac91-245">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cac91-247">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="cac91-247">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cac91-248">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooLinkedIn 查閱。</span><span class="sxs-lookup"><span data-stu-id="cac91-248">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Lookup.</span></span>

![指派使用者][200] 

<span data-ttu-id="cac91-250">**tooassign 許 Simon tooLinkedIn 查閱，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cac91-250">**tooassign Britta Simon tooLinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="cac91-251">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cac91-251">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="cac91-253">在 [hello] 應用程式清單中，選取**LinkedIn 查閱**。</span><span class="sxs-lookup"><span data-stu-id="cac91-253">In hello applications list, select **LinkedIn Lookup**.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="cac91-255">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="cac91-255">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="cac91-257">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cac91-257">Click **Add** button.</span></span> <span data-ttu-id="cac91-258">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cac91-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="cac91-260">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="cac91-260">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cac91-261">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cac91-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cac91-262">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cac91-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cac91-263">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="cac91-263">Testing single sign-on</span></span>

<span data-ttu-id="cac91-264">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="cac91-264">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cac91-265">當您按一下的 hello LinkedIn 查閱磚 hello 存取面板中時，您應該重新導向的 tooOrganizational 頁面具有 tooprovide 您個人的 LinkedIn 帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cac91-265">When you click hello LinkedIn Lookup tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="cac91-266">它會連結您的個人帳戶與您的 LinkedIn 商務帳戶。</span><span class="sxs-lookup"><span data-stu-id="cac91-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="cac91-267">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="cac91-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cac91-268">其他資源</span><span class="sxs-lookup"><span data-stu-id="cac91-268">Additional resources</span></span>

* [<span data-ttu-id="cac91-269">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cac91-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cac91-270">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="cac91-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

