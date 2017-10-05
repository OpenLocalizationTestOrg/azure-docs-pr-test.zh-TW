---
title: "教學課程：Azure Active Directory 與 ServiceChannel 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ServiceChannel 之間的單一登入。"
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
ms.openlocfilehash: 7e1dad18ff0ae9a9102b789b2cb32e7b96ed3d38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="23f66-103">教學課程：Azure Active Directory 與 ServiceChannel 整合</span><span class="sxs-lookup"><span data-stu-id="23f66-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="23f66-104">在本教學課程中，您會了解如何整合 ServiceChannel 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="23f66-104">In this tutorial, you learn how to integrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23f66-105">ServiceChannel 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="23f66-105">Integrating ServiceChannel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="23f66-106">您可以在 Azure AD 中控制可存取 ServiceChannel 的人員</span><span class="sxs-lookup"><span data-stu-id="23f66-106">You can control in Azure AD who has access to ServiceChannel</span></span>
- <span data-ttu-id="23f66-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 ServiceChannel (單一登入)</span><span class="sxs-lookup"><span data-stu-id="23f66-107">You can enable your users to automatically get signed-on to ServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="23f66-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="23f66-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="23f66-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="23f66-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23f66-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="23f66-110">Prerequisites</span></span>

<span data-ttu-id="23f66-111">若要設定 Azure AD 與 ServiceChannel 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="23f66-111">To configure Azure AD integration with ServiceChannel, you need the following items:</span></span>

- <span data-ttu-id="23f66-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="23f66-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23f66-113">已啟用 ServiceChannel 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="23f66-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23f66-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="23f66-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23f66-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="23f66-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23f66-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="23f66-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="23f66-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="23f66-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23f66-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="23f66-118">Scenario description</span></span>
<span data-ttu-id="23f66-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="23f66-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23f66-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="23f66-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23f66-121">從資源庫新增 ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="23f66-121">Adding ServiceChannel from the gallery</span></span>
2. <span data-ttu-id="23f66-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="23f66-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-the-gallery"></a><span data-ttu-id="23f66-123">從資源庫新增 ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="23f66-123">Adding ServiceChannel from the gallery</span></span>
<span data-ttu-id="23f66-124">若要設定將 ServiceChannel 整合到 Azure AD 中，您需要從資源庫將 ServiceChannel 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="23f66-124">To configure the integration of ServiceChannel into Azure AD, you need to add ServiceChannel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="23f66-125">**若要從資源庫新增 ServiceChannel，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="23f66-125">**To add ServiceChannel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="23f66-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="23f66-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="23f66-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="23f66-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="23f66-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="23f66-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="23f66-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="23f66-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="23f66-133">在搜尋方塊中，輸入 **ServiceChannel**。</span><span class="sxs-lookup"><span data-stu-id="23f66-133">In the search box, type **ServiceChannel**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="23f66-135">在結果窗格中，選取 [ServiceChannel]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="23f66-135">In the results panel, select **ServiceChannel**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="23f66-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="23f66-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="23f66-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 ServiceChannel 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="23f66-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="23f66-139">若要讓單一登入運作，Azure AD 必須知道 ServiceChannel 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="23f66-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceChannel is to a user in Azure AD.</span></span> <span data-ttu-id="23f66-140">換句話說，必須在 Azure AD 使用者和 ServiceChannel 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="23f66-140">In other words, a link relationship between an Azure AD user and the related user in ServiceChannel needs to be established.</span></span>

<span data-ttu-id="23f66-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 ServiceChannel 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="23f66-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceChannel.</span></span>

<span data-ttu-id="23f66-142">若要設定及測試對 ServiceChannel 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="23f66-142">To configure and test Azure AD single sign-on with ServiceChannel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="23f66-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="23f66-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="23f66-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="23f66-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="23f66-145">**[建立 ServiceChannel 測試使用者](#creating-a-servicechannel-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="23f66-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="23f66-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="23f66-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="23f66-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="23f66-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="23f66-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="23f66-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="23f66-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 ServiceChannel 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="23f66-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="23f66-150">**若要使用 ServiceChannel 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="23f66-150">**To configure Azure AD single sign-on with ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="23f66-151">在 Azure 管理入口網站的 [ServiceChannel] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="23f66-151">In the Azure Management portal, on the **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="23f66-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="23f66-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="23f66-155">在 [ServiceChannel 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="23f66-155">On the **ServiceChannel Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="23f66-157">a.</span><span class="sxs-lookup"><span data-stu-id="23f66-157">a.</span></span> <span data-ttu-id="23f66-158">在 [識別碼] 文字方塊中，以下列形式輸入值：`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="23f66-158">In the **Identifier** textbox, type the value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="23f66-159">b.</span><span class="sxs-lookup"><span data-stu-id="23f66-159">b.</span></span> <span data-ttu-id="23f66-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="23f66-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="23f66-161">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="23f66-161">Please note that these are not the real values.</span></span> <span data-ttu-id="23f66-162">您必須使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="23f66-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="23f66-163">在此建議您在 [識別碼] 中使用唯一的字串值。</span><span class="sxs-lookup"><span data-stu-id="23f66-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="23f66-164">請連絡 [ServiceChannel 支援小組](https://servicechannel.zendesk.com/hc/en-us)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="23f66-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) to get these values.</span></span>

4. <span data-ttu-id="23f66-165">ServiceChannel 應用程式需要特定格式的 SAML 判斷提示，所以您必須將自訂屬性對應新增至 SAML 權杖屬性設定。</span><span class="sxs-lookup"><span data-stu-id="23f66-165">Your ServiceChannel application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="23f66-166">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="23f66-166">The following screenshot shows an example for this.</span></span> <span data-ttu-id="23f66-167">**NameIdentifier(使用者識別碼)**是唯一的強制宣告，預設值是 **user.userprincipalname**，但 ServiceChannel 會需要此值對應至 **user.mail**。</span><span class="sxs-lookup"><span data-stu-id="23f66-167">**NameIdentifier(User Identifier)** is the only mandatory claim and the default value is **user.userprincipalname** but ServiceChannel expects this to be mapped with **user.mail**.</span></span> <span data-ttu-id="23f66-168">如果您打算啟用 Just In Time 使用者佈建，則應該新增下列宣告，如下所示。</span><span class="sxs-lookup"><span data-stu-id="23f66-168">If you are planning to enable Just In Time user provisioning, then you should add the following claims as shown below.</span></span> <span data-ttu-id="23f66-169">**角色**宣告需要對應到 **user.assignedroles**，其中包含使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="23f66-169">**Role** claim needs to be mapped to **user.assignedroles** which contains the role of the user.</span></span>  

    <span data-ttu-id="23f66-170">您可以參考[這裡](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example)的 ServiceChannel 指南，以取得宣告的詳細指引。</span><span class="sxs-lookup"><span data-stu-id="23f66-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="23f66-172">請按一下[這裡](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/)，以了解如何在 Azure AD 中設定**角色**</span><span class="sxs-lookup"><span data-stu-id="23f66-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) to know how to configure **Role** in Azure AD</span></span>

5. <span data-ttu-id="23f66-173">在 [使用者屬性] 區段中，按一下 [檢視及編輯所有其他使用者屬性]，然後設定屬性。</span><span class="sxs-lookup"><span data-stu-id="23f66-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span>

    | <span data-ttu-id="23f66-174">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="23f66-174">Attribute Name</span></span> | <span data-ttu-id="23f66-175">屬性值</span><span class="sxs-lookup"><span data-stu-id="23f66-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="23f66-176">角色</span><span class="sxs-lookup"><span data-stu-id="23f66-176">Role</span></span>| <span data-ttu-id="23f66-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="23f66-177">user.assignedroles</span></span> |

    <span data-ttu-id="23f66-178">a.</span><span class="sxs-lookup"><span data-stu-id="23f66-178">a.</span></span> <span data-ttu-id="23f66-179">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="23f66-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="23f66-182">b.</span><span class="sxs-lookup"><span data-stu-id="23f66-182">b.</span></span> <span data-ttu-id="23f66-183">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="23f66-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="23f66-184">c.</span><span class="sxs-lookup"><span data-stu-id="23f66-184">c.</span></span> <span data-ttu-id="23f66-185">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="23f66-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="23f66-186">d.</span><span class="sxs-lookup"><span data-stu-id="23f66-186">d.</span></span> <span data-ttu-id="23f66-187">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="23f66-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="23f66-188">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="23f66-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="23f66-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="23f66-190">Click **Save**.</span></span>

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="23f66-192">在 [ServiceChannel 組態] 區段上，按一下 [設定 ServiceChannel] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="23f66-192">On the **ServiceChannel Configuration** section, click **Configure ServiceChannel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="23f66-193">請記下 [快速參考] 區段中的 [SAML 實體識別碼]。</span><span class="sxs-lookup"><span data-stu-id="23f66-193">Please note the **SAML Enitity ID** from the **Quick Reference** section.</span></span>

9. <span data-ttu-id="23f66-194">若要在 **ServiceChannel** 端設定單一登入，您需要將已下載的**憑證 (Base64)**和 **SAML 實體識別碼**傳送給 [ServiceChannel 支援小組](https://servicechannel.zendesk.com/hc/en-us)。</span><span class="sxs-lookup"><span data-stu-id="23f66-194">To configure single sign-on on **ServiceChannel** side, you need to send the downloaded **certificate (Base64)** and **SAML Entity ID** to [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="23f66-195">他們將會設定妥當，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="23f66-195">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="23f66-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="23f66-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="23f66-197">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="23f66-197">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="23f66-199">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="23f66-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="23f66-200">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="23f66-200">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="23f66-202">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="23f66-202">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="23f66-204">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="23f66-204">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="23f66-206">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="23f66-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="23f66-208">a.</span><span class="sxs-lookup"><span data-stu-id="23f66-208">a.</span></span> <span data-ttu-id="23f66-209">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="23f66-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23f66-210">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="23f66-210">b.</span></span> <span data-ttu-id="23f66-211">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="23f66-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="23f66-212">c.</span><span class="sxs-lookup"><span data-stu-id="23f66-212">c.</span></span> <span data-ttu-id="23f66-213">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="23f66-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="23f66-214">d.</span><span class="sxs-lookup"><span data-stu-id="23f66-214">d.</span></span> <span data-ttu-id="23f66-215">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="23f66-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="23f66-216">建立 ServiceChannel 測試使用者</span><span class="sxs-lookup"><span data-stu-id="23f66-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="23f66-217">應用程式支援及時 (Just In Time) 使用者佈建，而在驗證之後，則會在應用程式中自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="23f66-217">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="23f66-218">如需完整的使用者佈建，請連絡 [ServiceChannel 支援小組](https://servicechannel.zendesk.com/hc/en-us)</span><span class="sxs-lookup"><span data-stu-id="23f66-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="23f66-219">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="23f66-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="23f66-220">在本節中，您會將 ServiceChannel 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="23f66-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceChannel.</span></span>

![指派使用者][200] 

<span data-ttu-id="23f66-222">**若要將 Britta Simon 指派到 ServiceChannel，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="23f66-222">**To assign Britta Simon to ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="23f66-223">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="23f66-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="23f66-225">在應用程式清單中，選取 [ServiceChannel]。</span><span class="sxs-lookup"><span data-stu-id="23f66-225">In the applications list, select **ServiceChannel**.</span></span>

    ![設定單一登入](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="23f66-227">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="23f66-227">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="23f66-229">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="23f66-229">Click **Add** button.</span></span> <span data-ttu-id="23f66-230">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="23f66-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="23f66-232">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="23f66-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="23f66-233">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="23f66-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="23f66-234">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="23f66-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="23f66-235">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="23f66-235">Testing single sign-on</span></span>

<span data-ttu-id="23f66-236">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="23f66-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="23f66-237">當您在存取面板中按一下 [ServiceChannel] 圖格時，應該會自動登入您的 ServiceChannel 應用程式。</span><span class="sxs-lookup"><span data-stu-id="23f66-237">When you click the ServiceChannel tile in the Access Panel, you should get automatically signed-on to your ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="23f66-238">其他資源</span><span class="sxs-lookup"><span data-stu-id="23f66-238">Additional resources</span></span>

* [<span data-ttu-id="23f66-239">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="23f66-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="23f66-240">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="23f66-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


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