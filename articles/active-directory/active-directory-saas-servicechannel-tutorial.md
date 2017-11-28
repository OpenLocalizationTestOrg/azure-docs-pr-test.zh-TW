---
title: "教學課程：Azure Active Directory 與 ServiceChannel 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ServiceChannel 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="8b403-103">教學課程：Azure Active Directory 與 ServiceChannel 整合</span><span class="sxs-lookup"><span data-stu-id="8b403-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="8b403-104">在此教學課程中，您學會如何 toointegrate ServiceChannel 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8b403-104">In this tutorial, you learn how toointegrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b403-105">與 Azure AD 整合 ServiceChannel 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="8b403-105">Integrating ServiceChannel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8b403-106">您可以控制存取 tooServiceChannel Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="8b403-106">You can control in Azure AD who has access tooServiceChannel</span></span>
- <span data-ttu-id="8b403-107">您可以啟用您的使用者 tooautomatically get 登入 tooServiceChannel （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="8b403-107">You can enable your users tooautomatically get signed-on tooServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b403-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="8b403-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="8b403-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8b403-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b403-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8b403-110">Prerequisites</span></span>

<span data-ttu-id="8b403-111">tooconfigure ServiceChannel 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="8b403-111">tooconfigure Azure AD integration with ServiceChannel, you need hello following items:</span></span>

- <span data-ttu-id="8b403-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8b403-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b403-113">已啟用 ServiceChannel 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8b403-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b403-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="8b403-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b403-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8b403-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b403-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="8b403-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8b403-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="8b403-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b403-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8b403-118">Scenario description</span></span>
<span data-ttu-id="8b403-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b403-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b403-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="8b403-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b403-121">ServiceChannel 加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="8b403-121">Adding ServiceChannel from hello gallery</span></span>
2. <span data-ttu-id="8b403-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8b403-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-hello-gallery"></a><span data-ttu-id="8b403-123">ServiceChannel 加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="8b403-123">Adding ServiceChannel from hello gallery</span></span>
<span data-ttu-id="8b403-124">tooconfigure hello 整合 ServiceChannel 到 Azure AD，您需要 tooadd ServiceChannel hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b403-124">tooconfigure hello integration of ServiceChannel into Azure AD, you need tooadd ServiceChannel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8b403-125">**tooadd ServiceChannel 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8b403-125">**tooadd ServiceChannel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b403-126">在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8b403-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8b403-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8b403-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8b403-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8b403-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8b403-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b403-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8b403-133">在 [hello] 搜尋方塊中，輸入**ServiceChannel**。</span><span class="sxs-lookup"><span data-stu-id="8b403-133">In hello search box, type **ServiceChannel**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="8b403-135">在 hello 結果 窗格中，選取  **ServiceChannel**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b403-135">In hello results panel, select **ServiceChannel**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b403-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8b403-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b403-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 ServiceChannel 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b403-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8b403-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 ServiceChannel 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="8b403-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceChannel is tooa user in Azure AD.</span></span> <span data-ttu-id="8b403-140">換句話說，Azure AD 使用者與 hello ServiceChannel 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="8b403-140">In other words, a link relationship between an Azure AD user and hello related user in ServiceChannel needs toobe established.</span></span>

<span data-ttu-id="8b403-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** ServiceChannel 中。</span><span class="sxs-lookup"><span data-stu-id="8b403-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceChannel.</span></span>

<span data-ttu-id="8b403-142">tooconfigure 及 ServiceChannel 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="8b403-142">tooconfigure and test Azure AD single sign-on with ServiceChannel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8b403-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="8b403-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8b403-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="8b403-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b403-145">**[建立測試使用者 ServiceChannel](#creating-a-servicechannel-test-user)**  -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="8b403-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="8b403-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b403-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b403-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="8b403-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8b403-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8b403-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8b403-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並在 ServiceChannel 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b403-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="8b403-150">**tooconfigure Azure AD 單一登入與 ServiceChannel，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8b403-150">**tooconfigure Azure AD single sign-on with ServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b403-151">在 hello Azure 管理入口網站上 hello **ServiceChannel**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="8b403-151">In hello Azure Management portal, on hello **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8b403-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b403-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="8b403-155">在 hello **ServiceChannel 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8b403-155">On hello **ServiceChannel Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="8b403-157">a.</span><span class="sxs-lookup"><span data-stu-id="8b403-157">a.</span></span> <span data-ttu-id="8b403-158">在 hello**識別碼**文字方塊中，做為型別 hello 值：`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="8b403-158">In hello **Identifier** textbox, type hello value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="8b403-159">b.</span><span class="sxs-lookup"><span data-stu-id="8b403-159">b.</span></span> <span data-ttu-id="8b403-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="8b403-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8b403-161">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="8b403-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="8b403-162">您有 tooupdate hello 實際的識別項和回覆 url 的這些值。</span><span class="sxs-lookup"><span data-stu-id="8b403-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="8b403-163">這裡我們建議您 toouse hello 唯一字串的值在 hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="8b403-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="8b403-164">請連絡[ServiceChannel 支援小組](https://servicechannel.zendesk.com/hc/en-us)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="8b403-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) tooget these values.</span></span>

4. <span data-ttu-id="8b403-165">ServiceChannel 應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 tooadd 自訂屬性對應 tooyour SAML token 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="8b403-165">Your ServiceChannel application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="8b403-166">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="8b403-166">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="8b403-167">**（使用者識別碼） NameIdentifier**為 hello 必要的宣告以及 hello 預設值是**user.userprincipalname**但 ServiceChannel 必須要有與對應此 toobe **user.mail**。</span><span class="sxs-lookup"><span data-stu-id="8b403-167">**NameIdentifier(User Identifier)** is hello only mandatory claim and hello default value is **user.userprincipalname** but ServiceChannel expects this toobe mapped with **user.mail**.</span></span> <span data-ttu-id="8b403-168">如果您打算 tooenable 只在即時使用者佈建，您應該加入 hello 下列宣告，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8b403-168">If you are planning tooenable Just In Time user provisioning, then you should add hello following claims as shown below.</span></span> <span data-ttu-id="8b403-169">**角色**宣告必須對應太 toobe**user.assignedroles**包含 hello hello 使用者角色。</span><span class="sxs-lookup"><span data-stu-id="8b403-169">**Role** claim needs toobe mapped too**user.assignedroles** which contains hello role of hello user.</span></span>  

    <span data-ttu-id="8b403-170">您可以參考[這裡](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example)的 ServiceChannel 指南，以取得宣告的詳細指引。</span><span class="sxs-lookup"><span data-stu-id="8b403-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="8b403-172">請按一下[這裡](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/)tooknow 如何 tooconfigure**角色**在 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="8b403-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow how tooconfigure **Role** in Azure AD</span></span>

5. <span data-ttu-id="8b403-173">在**使用者屬性**區段中，按一下**檢視和編輯所有其他使用者屬性**，並設定 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="8b403-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span>

    | <span data-ttu-id="8b403-174">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="8b403-174">Attribute Name</span></span> | <span data-ttu-id="8b403-175">屬性值</span><span class="sxs-lookup"><span data-stu-id="8b403-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="8b403-176">角色</span><span class="sxs-lookup"><span data-stu-id="8b403-176">Role</span></span>| <span data-ttu-id="8b403-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="8b403-177">user.assignedroles</span></span> |

    <span data-ttu-id="8b403-178">a.</span><span class="sxs-lookup"><span data-stu-id="8b403-178">a.</span></span> <span data-ttu-id="8b403-179">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="8b403-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="8b403-182">b.</span><span class="sxs-lookup"><span data-stu-id="8b403-182">b.</span></span> <span data-ttu-id="8b403-183">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="8b403-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8b403-184">c.</span><span class="sxs-lookup"><span data-stu-id="8b403-184">c.</span></span> <span data-ttu-id="8b403-185">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="8b403-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8b403-186">d.</span><span class="sxs-lookup"><span data-stu-id="8b403-186">d.</span></span> <span data-ttu-id="8b403-187">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8b403-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="8b403-188">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="8b403-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="8b403-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8b403-190">Click **Save**.</span></span>

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8b403-192">在 hello **ServiceChannel 組態**區段中，按一下**設定 ServiceChannel** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="8b403-192">On hello **ServiceChannel Configuration** section, click **Configure ServiceChannel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8b403-193">請注意 hello **SAML Enitity 識別碼**從 hello**快速參考**> 一節。</span><span class="sxs-lookup"><span data-stu-id="8b403-193">Please note hello **SAML Enitity ID** from hello **Quick Reference** section.</span></span>

9. <span data-ttu-id="8b403-194">tooconfigure 單一登入上**ServiceChannel**端，您需要下載 toosend hello**憑證 (Base64)**和**SAML 實體識別碼**太[ServiceChannel 支援小組](https://servicechannel.zendesk.com/hc/en-us)。</span><span class="sxs-lookup"><span data-stu-id="8b403-194">tooconfigure single sign-on on **ServiceChannel** side, you need toosend hello downloaded **certificate (Base64)** and **SAML Entity ID** too[ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="8b403-195">它們會設定此順序 toohave hello SAML SSO 連線兩端上正確設定。</span><span class="sxs-lookup"><span data-stu-id="8b403-195">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b403-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8b403-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b403-197">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8b403-197">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8b403-199">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8b403-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b403-200">在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8b403-200">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b403-202">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="8b403-202">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b403-204">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="8b403-204">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b403-206">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8b403-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b403-208">a.</span><span class="sxs-lookup"><span data-stu-id="8b403-208">a.</span></span> <span data-ttu-id="8b403-209">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8b403-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b403-210">b.</span><span class="sxs-lookup"><span data-stu-id="8b403-210">b.</span></span> <span data-ttu-id="8b403-211">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="8b403-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b403-212">c.</span><span class="sxs-lookup"><span data-stu-id="8b403-212">c.</span></span> <span data-ttu-id="8b403-213">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="8b403-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8b403-214">d.</span><span class="sxs-lookup"><span data-stu-id="8b403-214">d.</span></span> <span data-ttu-id="8b403-215">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8b403-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="8b403-216">建立 ServiceChannel 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8b403-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="8b403-217">應用程式支援恰好在即時使用者佈建，以及之後驗證的使用者將會在 hello 應用程式中自動建立。</span><span class="sxs-lookup"><span data-stu-id="8b403-217">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="8b403-218">如需完整的使用者佈建，請連絡 [ServiceChannel 支援小組](https://servicechannel.zendesk.com/hc/en-us)</span><span class="sxs-lookup"><span data-stu-id="8b403-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8b403-219">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="8b403-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8b403-220">在本節中，您可以授與他們存取 tooServiceChannel 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b403-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceChannel.</span></span>

![指派使用者][200] 

<span data-ttu-id="8b403-222">**tooassign 許 Simon tooServiceChannel，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8b403-222">**tooassign Britta Simon tooServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b403-223">在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8b403-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8b403-225">在 [hello] 應用程式清單中，選取**ServiceChannel**。</span><span class="sxs-lookup"><span data-stu-id="8b403-225">In hello applications list, select **ServiceChannel**.</span></span>

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="8b403-227">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="8b403-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8b403-229">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b403-229">Click **Add** button.</span></span> <span data-ttu-id="8b403-230">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8b403-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8b403-232">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="8b403-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8b403-233">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b403-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b403-234">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b403-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8b403-235">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8b403-235">Testing single sign-on</span></span>

<span data-ttu-id="8b403-236">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="8b403-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8b403-237">當您按一下 hello ServiceChannel 磚 hello 存取面板中的時，您應該取得自動登入 tooyour ServiceChannel 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b403-237">When you click hello ServiceChannel tile in hello Access Panel, you should get automatically signed-on tooyour ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b403-238">其他資源</span><span class="sxs-lookup"><span data-stu-id="8b403-238">Additional resources</span></span>

* [<span data-ttu-id="8b403-239">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b403-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b403-240">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8b403-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png