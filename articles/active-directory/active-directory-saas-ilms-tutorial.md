---
title: "教學課程：Azure Active Directory 與 iLMS 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 iLMS 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="afefc-103">教學課程：Azure Active Directory 與 iLMS 整合</span><span class="sxs-lookup"><span data-stu-id="afefc-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="afefc-104">在此教學課程中，您學會如何 toointegrate iLMS 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="afefc-104">In this tutorial, you learn how toointegrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="afefc-105">與 Azure AD 整合 iLMS 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="afefc-105">Integrating iLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="afefc-106">您可以控制存取 tooiLMS Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="afefc-106">You can control in Azure AD who has access tooiLMS</span></span>
- <span data-ttu-id="afefc-107">您可以啟用您的使用者 tooautomatically get 登入 tooiLMS （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="afefc-107">You can enable your users tooautomatically get signed-on tooiLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="afefc-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="afefc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="afefc-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="afefc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afefc-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="afefc-110">Prerequisites</span></span>

<span data-ttu-id="afefc-111">tooconfigure iLMS 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="afefc-111">tooconfigure Azure AD integration with iLMS, you need hello following items:</span></span>

- <span data-ttu-id="afefc-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="afefc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="afefc-113">啟用 iLMS 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="afefc-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="afefc-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="afefc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="afefc-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="afefc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="afefc-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="afefc-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="afefc-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="afefc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="afefc-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="afefc-118">Scenario description</span></span>
<span data-ttu-id="afefc-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="afefc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="afefc-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="afefc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="afefc-121">從 hello 圖庫加入 iLMS</span><span class="sxs-lookup"><span data-stu-id="afefc-121">Adding iLMS from hello gallery</span></span>
2. <span data-ttu-id="afefc-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="afefc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-hello-gallery"></a><span data-ttu-id="afefc-123">從 hello 圖庫加入 iLMS</span><span class="sxs-lookup"><span data-stu-id="afefc-123">Adding iLMS from hello gallery</span></span>
<span data-ttu-id="afefc-124">tooconfigure hello 整合 iLMS 到 Azure AD，您需要 tooadd iLMS hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="afefc-124">tooconfigure hello integration of iLMS into Azure AD, you need tooadd iLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="afefc-125">**tooadd iLMS 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="afefc-125">**tooadd iLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="afefc-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="afefc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="afefc-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="afefc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="afefc-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="afefc-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="afefc-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="afefc-131">tooadd new application, click **New application** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="afefc-133">在 [hello] 搜尋方塊中，輸入**iLMS**。</span><span class="sxs-lookup"><span data-stu-id="afefc-133">In hello search box, type **iLMS**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="afefc-135">在 hello 結果 窗格中，選取  **iLMS**，然後按一下 **新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="afefc-135">In hello results panel, select **iLMS**, then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="afefc-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="afefc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="afefc-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 iLMS 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="afefc-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="afefc-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 iLMS 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="afefc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in iLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="afefc-140">換句話說，Azure AD 使用者與 hello iLMS 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="afefc-140">In other words, a link relationship between an Azure AD user and hello related user in iLMS needs toobe established.</span></span>

<span data-ttu-id="afefc-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** iLMS 中。</span><span class="sxs-lookup"><span data-stu-id="afefc-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in iLMS.</span></span>

<span data-ttu-id="afefc-142">tooconfigure 及 iLMS 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="afefc-142">tooconfigure and test Azure AD single sign-on with iLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="afefc-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="afefc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="afefc-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="afefc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="afefc-145">**[建立測試使用者 iLMS](#creating-an-ilms-test-user)**  -toohave 是連結的 toohello Azure AD 表示她的 iLMS 的許 Simon 的對應項目。</span><span class="sxs-lookup"><span data-stu-id="afefc-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - toohave a counterpart of Britta Simon in iLMS that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="afefc-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="afefc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="afefc-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="afefc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="afefc-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="afefc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="afefc-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 iLMS 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="afefc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="afefc-150">**tooconfigure Azure AD 單一登入與 iLMS，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="afefc-150">**tooconfigure Azure AD single sign-on with iLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="afefc-151">在 Azure 入口網站上 hello hello **iLMS**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="afefc-151">In hello Azure portal, on hello **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="afefc-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="afefc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="afefc-155">在 hello **iLMS 網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="afefc-155">On hello **iLMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="afefc-157">a.</span><span class="sxs-lookup"><span data-stu-id="afefc-157">a.</span></span> <span data-ttu-id="afefc-158">在 hello**識別碼**文字方塊中，貼上 hello**識別碼**您複製的值**服務提供者**iLMS 系統管理入口網站中的 SAML 設定 區段。</span><span class="sxs-lookup"><span data-stu-id="afefc-158">In hello **Identifier** textbox, paste hello **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="afefc-159">b.</span><span class="sxs-lookup"><span data-stu-id="afefc-159">b.</span></span> <span data-ttu-id="afefc-160">在 [hello**回覆 URL**文字方塊中，貼上 hello**端點 (URL)**您複製的值**服務提供者**iLMS 擁有 hello 下列的系統管理員入口網站中的 SAML 設定] 區段模式`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="afefc-160">In hello **Reply URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having hello following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="afefc-161">這個 '123456' 是識別項的範例值。</span><span class="sxs-lookup"><span data-stu-id="afefc-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="afefc-162">請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="afefc-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="afefc-164">在 hello**登入 URL**文字方塊中，貼上 hello**端點 (URL)**您複製的值**服務提供者**SAML 設定在為 iLMS 管理入口網站中的區段`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="afefc-164">In hello **Sign-on URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="afefc-165">tooenable JIT 佈建，iLMS 應用程式預期 hello SAML 判斷提示以特定格式。</span><span class="sxs-lookup"><span data-stu-id="afefc-165">tooenable JIT provisioning, iLMS application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="afefc-166">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="afefc-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="afefc-167">您可以從 hello 管理這些屬性的 hello 值**使用者屬性**應用程式整合頁面上的一節。</span><span class="sxs-lookup"><span data-stu-id="afefc-167">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="afefc-168">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="afefc-168">hello following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="afefc-170">建立**部門、 區域**和**除法**屬性並新增 iLMS hello 的這些屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="afefc-170">Create **Department, Region** and **Division** attributes and add hello name of these attributes in iLMS.</span></span> <span data-ttu-id="afefc-171">上述的所有屬性都是必要屬性。</span><span class="sxs-lookup"><span data-stu-id="afefc-171">All these attributes shown above are required.</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="afefc-172">您有 tooenable**建立 Un-recognized 使用者帳戶**iLMS toomap 中這些屬性。</span><span class="sxs-lookup"><span data-stu-id="afefc-172">You have tooenable **Create Un-recognized User Account** in iLMS toomap these attributes.</span></span> <span data-ttu-id="afefc-173">請依照下列指示 hello[這裡](http://support.inspiredelearning.com/customer/portal/articles/2204526)tooget hello 屬性設定了解。</span><span class="sxs-lookup"><span data-stu-id="afefc-173">Follow hello instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget an idea on hello attributes configuration.</span></span>

6. <span data-ttu-id="afefc-174">在 hello**使用者屬性**區段 hello**單一登入** 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="afefc-174">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="afefc-175">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="afefc-175">Attribute Name</span></span> | <span data-ttu-id="afefc-176">屬性值</span><span class="sxs-lookup"><span data-stu-id="afefc-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="afefc-177">division</span><span class="sxs-lookup"><span data-stu-id="afefc-177">division</span></span> | <span data-ttu-id="afefc-178">user.department</span><span class="sxs-lookup"><span data-stu-id="afefc-178">user.department</span></span> |
    | <span data-ttu-id="afefc-179">region</span><span class="sxs-lookup"><span data-stu-id="afefc-179">region</span></span> | <span data-ttu-id="afefc-180">user.state</span><span class="sxs-lookup"><span data-stu-id="afefc-180">user.state</span></span> |
    | <span data-ttu-id="afefc-181">department</span><span class="sxs-lookup"><span data-stu-id="afefc-181">department</span></span> | <span data-ttu-id="afefc-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="afefc-182">user.jobtitle</span></span> |

    <span data-ttu-id="afefc-183">a.</span><span class="sxs-lookup"><span data-stu-id="afefc-183">a.</span></span> <span data-ttu-id="afefc-184">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="afefc-184">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="afefc-187">b.</span><span class="sxs-lookup"><span data-stu-id="afefc-187">b.</span></span> <span data-ttu-id="afefc-188">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="afefc-188">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="afefc-189">c.</span><span class="sxs-lookup"><span data-stu-id="afefc-189">c.</span></span> <span data-ttu-id="afefc-190">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="afefc-190">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="afefc-191">d.</span><span class="sxs-lookup"><span data-stu-id="afefc-191">d.</span></span> <span data-ttu-id="afefc-192">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="afefc-192">Click **Ok**</span></span>

7. <span data-ttu-id="afefc-193">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="afefc-193">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="afefc-195">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="afefc-195">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="afefc-197">在不同的網頁瀏覽器視窗中，登入 tooyour **iLMS 管理入口**身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="afefc-197">In a different web browser window, log in tooyour **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="afefc-198">按一下**SSO:SAML**下**設定**tooopen SAML 設定 索引標籤，並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="afefc-198">Click **SSO:SAML** under **Settings** tab tooopen SAML settings and perform hello following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="afefc-200">a.</span><span class="sxs-lookup"><span data-stu-id="afefc-200">a.</span></span> <span data-ttu-id="afefc-201">展開 hello**服務提供者**> 一節，並複製 hello**識別碼**和**端點 (URL)**值。</span><span class="sxs-lookup"><span data-stu-id="afefc-201">Expand hello **Service Provider** section and copy hello **Identifier** and **Endpoint (URL)** value.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="afefc-203">b.</span><span class="sxs-lookup"><span data-stu-id="afefc-203">b.</span></span> <span data-ttu-id="afefc-204">在 [識別提供者] 區段中，按一下 [匯入中繼資料]。</span><span class="sxs-lookup"><span data-stu-id="afefc-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="afefc-205">c.</span><span class="sxs-lookup"><span data-stu-id="afefc-205">c.</span></span> <span data-ttu-id="afefc-206">選取 hello**中繼資料**從 Azure 入口網站下載檔案**SAML 簽章憑證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="afefc-206">Select hello **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="afefc-208">d.</span><span class="sxs-lookup"><span data-stu-id="afefc-208">d.</span></span> <span data-ttu-id="afefc-209">如果您想 tooenable JIT 為佈建 toocreate iLMS 帳戶取消-辨識使用者，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="afefc-209">If you want tooenable JIT provisioning toocreate iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="afefc-210">請勾選 [建立無法辨識的使用者帳戶]。</span><span class="sxs-lookup"><span data-stu-id="afefc-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="afefc-212">Azure AD 與 iLMS 中的 hello 屬性會對應 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="afefc-212">Map hello attributes in Azure AD with hello attributes in iLMS.</span></span> <span data-ttu-id="afefc-213">在 hello 屬性資料行，指定 hello 屬性名稱或 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="afefc-213">In hello attribute column, specify hello attributes name or hello default value.</span></span>

    <span data-ttu-id="afefc-214">e.</span><span class="sxs-lookup"><span data-stu-id="afefc-214">e.</span></span> <span data-ttu-id="afefc-215">跳過**商務規則**索引標籤，然後執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="afefc-215">Go too**Business Rules** tab and perform hello following steps:</span></span> 
        
       ![設定單一登入](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="afefc-217">請檢查**建立 Un-recognized 區域、 單位和部門**toocreate 區域，以及不存在時的單一登入 hello 的部門。</span><span class="sxs-lookup"><span data-stu-id="afefc-217">Check **Create Un-recognized Regions, Divisions and Departments** toocreate Regions, Divisions, and Departments that do not already exist at hello time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="afefc-218">請檢查**更新使用者設定檔期間登入**toospecify 是否 hello 使用者設定檔會更新每個單一登入。</span><span class="sxs-lookup"><span data-stu-id="afefc-218">Check **Update User Profile During Sign-in** toospecify whether hello user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="afefc-219">如果 hello **「 更新空白值的非必要欄位在使用者設定檔 」**核取選項，選擇性的設定檔的欄位空白時登入將也會導致 hello 使用者 iLMS 設定檔 toocontain 空白值，這些欄位。</span><span class="sxs-lookup"><span data-stu-id="afefc-219">If hello **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause hello user’s iLMS profile toocontain blank values for those fields.</span></span>
        
       - <span data-ttu-id="afefc-220">請檢查**傳送錯誤通知電子郵件**，然後輸入 hello 電子郵件的 hello 使用者希望 tooreceive hello 錯誤通知的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="afefc-220">Check **Send Error Notification Email** and enter hello email of hello user where you want tooreceive hello error notification email.</span></span>

11. <span data-ttu-id="afefc-221">按一下**儲存**按鈕 toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="afefc-221">Click **Save** button toosave hello settings.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="afefc-223">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="afefc-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="afefc-224">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="afefc-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="afefc-225">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="afefc-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="afefc-226">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="afefc-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="afefc-227">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="afefc-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="afefc-229">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="afefc-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="afefc-230">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="afefc-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="afefc-232">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="afefc-232">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="afefc-234">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="afefc-234">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="afefc-236">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="afefc-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="afefc-238">a.</span><span class="sxs-lookup"><span data-stu-id="afefc-238">a.</span></span> <span data-ttu-id="afefc-239">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="afefc-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="afefc-240">b.</span><span class="sxs-lookup"><span data-stu-id="afefc-240">b.</span></span> <span data-ttu-id="afefc-241">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="afefc-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="afefc-242">c.</span><span class="sxs-lookup"><span data-stu-id="afefc-242">c.</span></span> <span data-ttu-id="afefc-243">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="afefc-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="afefc-244">d.</span><span class="sxs-lookup"><span data-stu-id="afefc-244">d.</span></span> <span data-ttu-id="afefc-245">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="afefc-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="afefc-246">建立 iLMS 測試使用者</span><span class="sxs-lookup"><span data-stu-id="afefc-246">Creating an iLMS test user</span></span>

<span data-ttu-id="afefc-247">應用程式支援恰好在即時使用者佈建，以及之後驗證使用者會自動建立 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="afefc-247">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="afefc-248">JIT 也能運作，如果您已按下 hello**建立 Un-recognized 使用者帳戶**iLMS 系統管理入口網站在 SAML 組態設定期間的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="afefc-248">JIT will work, if you have clicked hello **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="afefc-249">若要手動 toocreate 使用者，然後依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="afefc-249">If you need toocreate an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="afefc-250">系統管理員身分登入 tooyour iLMS 公司網站。</span><span class="sxs-lookup"><span data-stu-id="afefc-250">Log in tooyour iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="afefc-251">按一下**「 註冊使用者 」**下**使用者**索引標籤上 tooopen**註冊使用者**頁面。</span><span class="sxs-lookup"><span data-stu-id="afefc-251">Click **“Register User”** under **Users** tab tooopen **Register User** page.</span></span> 
   
   ![新增員工](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="afefc-253">在 hello **「 註冊使用者 」**頁面上，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="afefc-253">On hello **“Register User”** page, perform hello following steps.</span></span>

    ![新增員工](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="afefc-255">a.</span><span class="sxs-lookup"><span data-stu-id="afefc-255">a.</span></span> <span data-ttu-id="afefc-256">在 hello**名字**文字方塊中，型別 hello 名字許。</span><span class="sxs-lookup"><span data-stu-id="afefc-256">In hello **First Name** textbox, type hello first name Britta.</span></span>
   
    <span data-ttu-id="afefc-257">b.</span><span class="sxs-lookup"><span data-stu-id="afefc-257">b.</span></span> <span data-ttu-id="afefc-258">在 hello**姓氏**文字方塊中，型別 hello 姓氏 Simon。</span><span class="sxs-lookup"><span data-stu-id="afefc-258">In hello **Last Name** textbox, type hello last name Simon.</span></span>

    <span data-ttu-id="afefc-259">c.</span><span class="sxs-lookup"><span data-stu-id="afefc-259">c.</span></span> <span data-ttu-id="afefc-260">在 [hello**電子郵件識別碼**許 Simon 帳戶類型 hello 電子郵件地址] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="afefc-260">In hello **Email ID** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="afefc-261">d.</span><span class="sxs-lookup"><span data-stu-id="afefc-261">d.</span></span> <span data-ttu-id="afefc-262">在 hello**區域**下拉式清單中，選取 hello 區域的值。</span><span class="sxs-lookup"><span data-stu-id="afefc-262">In hello **Region** dropdown, select hello value for region.</span></span>

    <span data-ttu-id="afefc-263">e.</span><span class="sxs-lookup"><span data-stu-id="afefc-263">e.</span></span> <span data-ttu-id="afefc-264">在 hello**除法**下拉式清單中，選取 hello 除數的值。</span><span class="sxs-lookup"><span data-stu-id="afefc-264">In hello **Division** dropdown, select hello value for division.</span></span>

    <span data-ttu-id="afefc-265">f.</span><span class="sxs-lookup"><span data-stu-id="afefc-265">f.</span></span> <span data-ttu-id="afefc-266">在 hello**部門**下拉式清單中，選取 hello 部門的值。</span><span class="sxs-lookup"><span data-stu-id="afefc-266">In hello **Department** dropdown, select hello value for department.</span></span>

    <span data-ttu-id="afefc-267">g.</span><span class="sxs-lookup"><span data-stu-id="afefc-267">g.</span></span> <span data-ttu-id="afefc-268">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="afefc-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="afefc-269">您可以透過選取傳送註冊郵件 toouser**傳送註冊郵件**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="afefc-269">You can send registration mail toouser by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="afefc-270">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="afefc-270">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="afefc-271">在本節中，您可以授與他們存取 tooiLMS 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="afefc-271">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooiLMS.</span></span>

![指派使用者][200] 

<span data-ttu-id="afefc-273">**tooassign 許 Simon tooiLMS，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="afefc-273">**tooassign Britta Simon tooiLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="afefc-274">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="afefc-274">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="afefc-276">在 [hello] 應用程式清單中，選取**iLMS**。</span><span class="sxs-lookup"><span data-stu-id="afefc-276">In hello applications list, select **iLMS**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="afefc-278">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="afefc-278">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="afefc-280">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="afefc-280">Click **Add** button.</span></span> <span data-ttu-id="afefc-281">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="afefc-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="afefc-283">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="afefc-283">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="afefc-284">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="afefc-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="afefc-285">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="afefc-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="afefc-286">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="afefc-286">Testing single sign-on</span></span>

<span data-ttu-id="afefc-287">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="afefc-287">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="afefc-288">當您按一下的 hello iLMS 磚 hello 存取面板中時，您應該取得自動登入 tooyour iLMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="afefc-288">When you click hello iLMS tile in hello Access Panel, you should get automatically signed-on tooyour iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="afefc-289">其他資源</span><span class="sxs-lookup"><span data-stu-id="afefc-289">Additional resources</span></span>

* [<span data-ttu-id="afefc-290">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="afefc-290">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="afefc-291">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="afefc-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

