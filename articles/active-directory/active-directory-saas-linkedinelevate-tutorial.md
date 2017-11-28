---
title: "教學課程：Azure Active Directory 與 LinkedIn Elevate 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與之間 LinkedIn 提高權限。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="dffd9-103">教學課程：Azure Active Directory 與 LinkedIn Elevate 整合</span><span class="sxs-lookup"><span data-stu-id="dffd9-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="dffd9-104">在此教學課程中，您學會如何 toointegrate LinkedIn 提高權限與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="dffd9-104">In this tutorial, you learn how toointegrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dffd9-105">整合與 Azure AD 的 LinkedIn 提高權限可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="dffd9-105">Integrating LinkedIn Elevate with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dffd9-106">您可以控制存取 tooLinkedIn 提高權限的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="dffd9-106">You can control in Azure AD who has access tooLinkedIn Elevate</span></span>
- <span data-ttu-id="dffd9-107">您可以啟用您的使用者 tooautomatically get 登入 tooLinkedIn 提高權限 （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="dffd9-107">You can enable your users tooautomatically get signed-on tooLinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dffd9-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="dffd9-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="dffd9-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="dffd9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dffd9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="dffd9-110">Prerequisites</span></span>

<span data-ttu-id="dffd9-111">tooconfigure 與 LinkedIn 提高權限的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="dffd9-111">tooconfigure Azure AD integration with LinkedIn Elevate, you need hello following items:</span></span>

- <span data-ttu-id="dffd9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dffd9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dffd9-113">啟用 LinkedIn Elevate 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dffd9-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dffd9-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="dffd9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dffd9-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="dffd9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dffd9-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="dffd9-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="dffd9-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="dffd9-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dffd9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="dffd9-118">Scenario description</span></span>
<span data-ttu-id="dffd9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dffd9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dffd9-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="dffd9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dffd9-121">從 hello 組件庫中加入 LinkedIn 提高權限</span><span class="sxs-lookup"><span data-stu-id="dffd9-121">Adding LinkedIn Elevate from hello gallery</span></span>
2. <span data-ttu-id="dffd9-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dffd9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-hello-gallery"></a><span data-ttu-id="dffd9-123">從 hello 組件庫中加入 LinkedIn 提高權限</span><span class="sxs-lookup"><span data-stu-id="dffd9-123">Adding LinkedIn Elevate from hello gallery</span></span>
<span data-ttu-id="dffd9-124">tooconfigure hello 整合 LinkedIn 提高到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd LinkedIn 提高權限。</span><span class="sxs-lookup"><span data-stu-id="dffd9-124">tooconfigure hello integration of LinkedIn Elevate into Azure AD, you need tooadd LinkedIn Elevate from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dffd9-125">**tooadd LinkedIn 提升從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dffd9-125">**tooadd LinkedIn Elevate from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dffd9-126">在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="dffd9-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dffd9-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dffd9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dffd9-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dffd9-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="dffd9-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="dffd9-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="dffd9-133">在 [hello] 搜尋方塊中，輸入**LinkedIn 提高**。</span><span class="sxs-lookup"><span data-stu-id="dffd9-133">In hello search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="dffd9-134">從 結果 窗格，按一下  **LinkedIn 提高**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffd9-134">From results panel, click **LinkedIn Elevate** tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dffd9-136">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dffd9-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dffd9-137">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 LinkedIn Elevate 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dffd9-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dffd9-138">單一登入 toowork，Azure AD 需要 tooknow hello 對應項目中 LinkedIn 提高權限的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="dffd9-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Elevate is tooa user in Azure AD.</span></span> <span data-ttu-id="dffd9-139">換句話說，Azure AD 使用者與 hello 中 LinkedIn 提高權限的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="dffd9-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Elevate needs toobe established.</span></span>

<span data-ttu-id="dffd9-140">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**中 LinkedIn 提高權限。</span><span class="sxs-lookup"><span data-stu-id="dffd9-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="dffd9-141">tooconfigure 及測試 Azure AD 單一登入與 LinkedIn 提高權限，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="dffd9-141">tooconfigure and test Azure AD single sign-on with LinkedIn Elevate, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dffd9-142">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="dffd9-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dffd9-143">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="dffd9-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dffd9-144">**[建立測試使用者 LinkedIn 提高](#creating-a-linkedin-elevate-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="dffd9-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="dffd9-145">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dffd9-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dffd9-146">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="dffd9-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dffd9-147">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dffd9-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dffd9-148">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並 LinkedIn 提高應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="dffd9-148">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="dffd9-149">**tooconfigure Azure AD 單一登入與 LinkedIn 提高權限，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dffd9-149">**tooconfigure Azure AD single sign-on with LinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="dffd9-150">在 hello Azure 管理入口網站上 hello **LinkedIn 提高**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="dffd9-150">In hello Azure Management portal, on hello **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="dffd9-152">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dffd9-152">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="dffd9-154">在不同的網頁瀏覽器視窗中，以系統管理員身分的登入 tooyour LinkedIn 提高租用戶。</span><span class="sxs-lookup"><span data-stu-id="dffd9-154">In a different web browser window, sign-on tooyour LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="dffd9-155">在 [帳戶中心] 中，按一下 [設定] 底下的 [全域設定]。</span><span class="sxs-lookup"><span data-stu-id="dffd9-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="dffd9-156">此外，選取**提高權限的提升 AAD 測試**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="dffd9-156">Also, select **Elevate - Elevate AAD Test** from hello dropdown list.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="dffd9-158">按一下**或按一下這裡 tooload 並複製個別欄位從 hello 表單**和複製**實體識別碼**和**判斷提示取用者存取 (ACS) Url**</span><span class="sxs-lookup"><span data-stu-id="dffd9-158">Click on **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="dffd9-160">在 Azure 入口網站，在**LinkedIn 提高權限的網域和 Url**，執行下列步驟，如果您想 tooconfigure SSO hello 中**IdP 初始化**模式</span><span class="sxs-lookup"><span data-stu-id="dffd9-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="dffd9-162">a.</span><span class="sxs-lookup"><span data-stu-id="dffd9-162">a.</span></span> <span data-ttu-id="dffd9-163">在 hello**識別碼**文字方塊中，輸入 hello**實體識別碼**從 LinkedIn 入口網站複製</span><span class="sxs-lookup"><span data-stu-id="dffd9-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="dffd9-164">b.</span><span class="sxs-lookup"><span data-stu-id="dffd9-164">b.</span></span> <span data-ttu-id="dffd9-165">在 hello**回覆 URL**文字方塊中，輸入 hello**判斷提示取用者存取 (ACS) Url**從 LinkedIn 入口網站複製</span><span class="sxs-lookup"><span data-stu-id="dffd9-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="dffd9-166">如果您想 tooconfigure SSO 中**SP 起始**，然後按一下 顯示進階的 URL hello 組態區段中的設定選項，並設定 hello 登入 URL，以下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="dffd9-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="dffd9-168">LinkedIn 提高應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 tooadd 自訂屬性對應 tooyour SAML token 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="dffd9-168">Your LinkedIn Elevate application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="dffd9-169">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="dffd9-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="dffd9-170">hello 預設值是**使用者識別碼**是**user.userprincipalname**但 LinkedIn 提高預期這個 toobe hello 使用者的電子郵件地址的對應。</span><span class="sxs-lookup"><span data-stu-id="dffd9-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="dffd9-171">您可以使用該**user.mail**屬性從 hello 清單或使用您組織的組態為基礎的 hello 適當的屬性值。</span><span class="sxs-lookup"><span data-stu-id="dffd9-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="dffd9-173">在**使用者屬性**區段中，按一下**檢視和編輯所有其他使用者屬性**，並設定 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="dffd9-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="dffd9-174">您需要另一個宣告名為 tooadd**部門**和 hello 值必須對應太 toobe**user.department**。</span><span class="sxs-lookup"><span data-stu-id="dffd9-174">You need tooadd another claim named **department** and hello value needs toobe mapped too**user.department**.</span></span>

    | <span data-ttu-id="dffd9-175">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="dffd9-175">Attribute Name</span></span> | <span data-ttu-id="dffd9-176">屬性值</span><span class="sxs-lookup"><span data-stu-id="dffd9-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="dffd9-177">department</span><span class="sxs-lookup"><span data-stu-id="dffd9-177">department</span></span>| <span data-ttu-id="dffd9-178">user.department</span><span class="sxs-lookup"><span data-stu-id="dffd9-178">user.department</span></span> |

      ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="dffd9-180">a.</span><span class="sxs-lookup"><span data-stu-id="dffd9-180">a.</span></span> <span data-ttu-id="dffd9-181">按一下 新增屬性 tooopen hello 屬性詳細資料頁面上的加入 hello 部門屬性所示以下-</span><span class="sxs-lookup"><span data-stu-id="dffd9-181">Click on Add attribute tooopen hello attribute details page add hello department attribute as shown below-</span></span>

      ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="dffd9-183">b.</span><span class="sxs-lookup"><span data-stu-id="dffd9-183">b.</span></span> <span data-ttu-id="dffd9-184">按一下**確定**toosave hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="dffd9-184">Click on **Ok** toosave hello attribute.</span></span>

      <span data-ttu-id="dffd9-185">c.</span><span class="sxs-lookup"><span data-stu-id="dffd9-185">c.</span></span> <span data-ttu-id="dffd9-186">變更 hello 屬性名稱的 hello **emailaddress**太**電子郵件**。</span><span class="sxs-lookup"><span data-stu-id="dffd9-186">Change hello name of hello attribute **emailaddress** too**email**.</span></span>


10. <span data-ttu-id="dffd9-187">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="dffd9-187">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="dffd9-189">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="dffd9-189">Click **Save**.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="dffd9-191">跳過**LinkedIn 的管理設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="dffd9-191">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="dffd9-192">上傳您剛才下載的 hello Azure 入口網站上 hello 上載 XML 檔案的選項即可 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="dffd9-192">Upload hello XML file you just downloaded from hello Azure portal by clicking on hello Upload XML file option.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="dffd9-194">按一下**上**tooenable SSO。</span><span class="sxs-lookup"><span data-stu-id="dffd9-194">Click **On** tooenable SSO.</span></span> <span data-ttu-id="dffd9-195">SSO 狀態會變更從**未連接**太**已連線**</span><span class="sxs-lookup"><span data-stu-id="dffd9-195">SSO status will change from **Not Connected** too**Connected**</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dffd9-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="dffd9-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="dffd9-198">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="dffd9-198">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="dffd9-200">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dffd9-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dffd9-201">在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="dffd9-201">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dffd9-203">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="dffd9-203">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dffd9-205">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="dffd9-205">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dffd9-207">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="dffd9-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dffd9-209">a.</span><span class="sxs-lookup"><span data-stu-id="dffd9-209">a.</span></span> <span data-ttu-id="dffd9-210">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="dffd9-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dffd9-211">b.</span><span class="sxs-lookup"><span data-stu-id="dffd9-211">b.</span></span> <span data-ttu-id="dffd9-212">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="dffd9-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dffd9-213">c.</span><span class="sxs-lookup"><span data-stu-id="dffd9-213">c.</span></span> <span data-ttu-id="dffd9-214">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="dffd9-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dffd9-215">d.</span><span class="sxs-lookup"><span data-stu-id="dffd9-215">d.</span></span> <span data-ttu-id="dffd9-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="dffd9-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="dffd9-217">建立 LinkedIn Elevate 測試使用者</span><span class="sxs-lookup"><span data-stu-id="dffd9-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="dffd9-218">連結的提高權限的應用程式支援恰好在即時使用者佈建，以及之後驗證的使用者將會在 hello 應用程式中自動建立。</span><span class="sxs-lookup"><span data-stu-id="dffd9-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="dffd9-219">Hello LinkedIn 提高入口網站的翻轉 hello 交換器上 hello 管理設定 頁面上**自動指派的授權**tooactive tooenable 恰好即時佈建，而這也會指派授權 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="dffd9-219">On hello admin settings page on hello LinkedIn Elevate portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>

   ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dffd9-221">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="dffd9-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dffd9-222">在本節中，以啟用許 Simon toouse Azure 單一登入授與他們存取 tooLinkedIn 提高權限。</span><span class="sxs-lookup"><span data-stu-id="dffd9-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLinkedIn Elevate.</span></span>

![指派使用者][200] 

<span data-ttu-id="dffd9-224">**tooassign 許 Simon tooLinkedIn 提高權限，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dffd9-224">**tooassign Britta Simon tooLinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="dffd9-225">在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dffd9-225">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="dffd9-227">在 [hello] 應用程式清單中，選取**LinkedIn 提高**。</span><span class="sxs-lookup"><span data-stu-id="dffd9-227">In hello applications list, select **LinkedIn Elevate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="dffd9-229">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="dffd9-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="dffd9-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dffd9-231">Click **Add** button.</span></span> <span data-ttu-id="dffd9-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="dffd9-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="dffd9-234">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="dffd9-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dffd9-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dffd9-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dffd9-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dffd9-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dffd9-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="dffd9-237">Testing single sign-on</span></span>

<span data-ttu-id="dffd9-238">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="dffd9-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dffd9-239">當您按一下 hello LinkedIn 提高並排顯示 hello 存取面板中的時，您應該取得 hello Azure 登入頁面和在之後成功登入，您應該取得 LinkedIn 提高應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffd9-239">When you click hello LinkedIn Elevate tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dffd9-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="dffd9-240">Additional resources</span></span>

* [<span data-ttu-id="dffd9-241">教學課程︰以 Azure Active Directory 設定自動使用者佈建的 LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="dffd9-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="dffd9-242">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dffd9-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dffd9-243">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="dffd9-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
