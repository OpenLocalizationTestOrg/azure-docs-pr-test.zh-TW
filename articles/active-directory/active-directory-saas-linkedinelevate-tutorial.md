---
title: "教學課程：Azure Active Directory 與 LinkedIn Elevate 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 LinkedIn Elevate 之間的單一登入。"
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
ms.openlocfilehash: 5336543e06d60be555722a615568b12048c2aa2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="11806-103">教學課程：Azure Active Directory 與 LinkedIn Elevate 整合</span><span class="sxs-lookup"><span data-stu-id="11806-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="11806-104">在本教學課程中，您將了解如何整合 LinkedIn Elevate 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="11806-104">In this tutorial, you learn how to integrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11806-105">LinkedIn Elevate 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="11806-105">Integrating LinkedIn Elevate with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="11806-106">您可以在 Azure AD 中控制可存取 LinkedIn Elevate 的人員</span><span class="sxs-lookup"><span data-stu-id="11806-106">You can control in Azure AD who has access to LinkedIn Elevate</span></span>
- <span data-ttu-id="11806-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 LinkedIn Elevate (單一登入)</span><span class="sxs-lookup"><span data-stu-id="11806-107">You can enable your users to automatically get signed-on to LinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11806-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="11806-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="11806-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="11806-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11806-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="11806-110">Prerequisites</span></span>

<span data-ttu-id="11806-111">若要設定 Azure AD 與 LinkedIn Elevate 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="11806-111">To configure Azure AD integration with LinkedIn Elevate, you need the following items:</span></span>

- <span data-ttu-id="11806-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="11806-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11806-113">啟用 LinkedIn Elevate 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="11806-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11806-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="11806-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11806-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="11806-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11806-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="11806-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="11806-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="11806-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11806-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="11806-118">Scenario description</span></span>
<span data-ttu-id="11806-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11806-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11806-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="11806-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11806-121">從資源庫新增 LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="11806-121">Adding LinkedIn Elevate from the gallery</span></span>
2. <span data-ttu-id="11806-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="11806-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-the-gallery"></a><span data-ttu-id="11806-123">從資源庫新增 LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="11806-123">Adding LinkedIn Elevate from the gallery</span></span>
<span data-ttu-id="11806-124">若要設定將 LinkedIn Elevate 整合到 Azure AD 中，您需要從資源庫將 LinkedIn Elevate 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="11806-124">To configure the integration of LinkedIn Elevate into Azure AD, you need to add LinkedIn Elevate from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="11806-125">**若要從資源庫新增 LinkedIn Elevate，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="11806-125">**To add LinkedIn Elevate from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="11806-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="11806-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="11806-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="11806-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="11806-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="11806-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="11806-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11806-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="11806-133">在搜尋方塊中，輸入 **LinkedIn Elevate**。</span><span class="sxs-lookup"><span data-stu-id="11806-133">In the search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="11806-134">從結果面板中，按一下 [LinkedIn Elevate] 以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="11806-134">From results panel, click **LinkedIn Elevate** to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11806-136">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="11806-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="11806-137">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 LinkedIn Elevate 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11806-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11806-138">若要讓單一登入能夠運作，Azure AD 必須知道 LinkedIn Elevate 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="11806-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Elevate is to a user in Azure AD.</span></span> <span data-ttu-id="11806-139">換句話說，必須在 Azure AD 使用者和 LinkedIn Elevate 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="11806-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Elevate needs to be established.</span></span>

<span data-ttu-id="11806-140">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 LinkedIn Elevate 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="11806-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="11806-141">若要設定及測試與 LinkedIn Elevate 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="11806-141">To configure and test Azure AD single sign-on with LinkedIn Elevate, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="11806-142">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="11806-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="11806-143">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11806-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11806-144">**[建立 LinkedIn Elevate 測試使用者](#creating-a-linkedin-elevate-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11806-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="11806-145">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11806-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11806-146">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="11806-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11806-147">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="11806-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11806-148">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 LinkedIn Elevate 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="11806-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="11806-149">**若要設定與 LinkedIn Elevate 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="11806-149">**To configure Azure AD single sign-on with LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="11806-150">在 Azure 管理入口網站的 [LinkedIn Elevate] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="11806-150">In the Azure Management portal, on the **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="11806-152">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="11806-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="11806-154">在不同的網頁瀏覽器視窗中，以管理員身分登入您的 LinkedIn Elevate 租用戶。</span><span class="sxs-lookup"><span data-stu-id="11806-154">In a different web browser window, sign-on to your LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="11806-155">在 [帳戶中心] 中，按一下 [設定] 底下的 [全域設定]。</span><span class="sxs-lookup"><span data-stu-id="11806-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="11806-156">此外，從下拉式清單選取 [提升 - 提升 AAD 測試]。</span><span class="sxs-lookup"><span data-stu-id="11806-156">Also, select **Elevate - Elevate AAD Test** from the dropdown list.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="11806-158">按一下 **，或按一下「這裡」以從表單**  載入和複製個別欄位，並且複製 [實體 ID] 和 [判斷提示取用者存取 (ACS) URL]</span><span class="sxs-lookup"><span data-stu-id="11806-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="11806-160">如果您想要在 **IDP 起始**模式中設定 SSO，請在 Azure 入口網站的 [LinkedIn Elevate 網域和 URL] 底下執行下列步驟</span><span class="sxs-lookup"><span data-stu-id="11806-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="11806-162">a.</span><span class="sxs-lookup"><span data-stu-id="11806-162">a.</span></span> <span data-ttu-id="11806-163">在 [識別碼] 文字方塊中，輸入從 LinkedIn 入口網站複製的 [實體 ID]</span><span class="sxs-lookup"><span data-stu-id="11806-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="11806-164">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="11806-164">b.</span></span> <span data-ttu-id="11806-165">在 [回覆 URL] 文字方塊中，輸入從 LinkedIn 入口網站複製的 [判斷提示取用者存取 (ACS) URL]</span><span class="sxs-lookup"><span data-stu-id="11806-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="11806-166">如果您想要在 **SP 起始**中設定 SSO，則在組態區段中按一下 [顯示進階 URL] 設定，然後使用下列模式設定登入 URL：</span><span class="sxs-lookup"><span data-stu-id="11806-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="11806-168">LinkedIn Elevate 應用程式需要特定格式的 SAML 判斷提示，要求您將自訂屬性對應新增到您的 SAML 權杖屬性組態。</span><span class="sxs-lookup"><span data-stu-id="11806-168">Your LinkedIn Elevate application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="11806-169">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="11806-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="11806-170">[使用者識別碼] 的預設值是 **user.userprincipalname**，但是 LinkedIn Elevate 預期它是與使用者電子郵件地址對應的值。</span><span class="sxs-lookup"><span data-stu-id="11806-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="11806-171">對此您可以使用清單中的 **user.mail** 屬性，或者根據組織組態使用適當的屬性值。</span><span class="sxs-lookup"><span data-stu-id="11806-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="11806-173">在 [使用者屬性] 區段中，按一下 [檢視及編輯所有其他使用者屬性]，然後設定屬性。</span><span class="sxs-lookup"><span data-stu-id="11806-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="11806-174">您必須新增名為**部門**的另一個宣告，且值必須對應至 **user.department**。</span><span class="sxs-lookup"><span data-stu-id="11806-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span></span>

    | <span data-ttu-id="11806-175">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="11806-175">Attribute Name</span></span> | <span data-ttu-id="11806-176">屬性值</span><span class="sxs-lookup"><span data-stu-id="11806-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="11806-177">department</span><span class="sxs-lookup"><span data-stu-id="11806-177">department</span></span>| <span data-ttu-id="11806-178">user.department</span><span class="sxs-lookup"><span data-stu-id="11806-178">user.department</span></span> |

      ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="11806-180">a.</span><span class="sxs-lookup"><span data-stu-id="11806-180">a.</span></span> <span data-ttu-id="11806-181">按一下 [新增屬性]，以開啟屬性的詳細資料頁面，如下所示新增部門屬性</span><span class="sxs-lookup"><span data-stu-id="11806-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span></span>

      ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="11806-183">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="11806-183">b.</span></span> <span data-ttu-id="11806-184">按一下 [確定] 儲存屬性。</span><span class="sxs-lookup"><span data-stu-id="11806-184">Click on **Ok** to save the attribute.</span></span>

      <span data-ttu-id="11806-185">c.</span><span class="sxs-lookup"><span data-stu-id="11806-185">c.</span></span> <span data-ttu-id="11806-186">將 **emailaddress** 屬性的名稱變更為 **email**。</span><span class="sxs-lookup"><span data-stu-id="11806-186">Change the name of the attribute **emailaddress** to **email**.</span></span>


10. <span data-ttu-id="11806-187">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="11806-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="11806-189">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="11806-189">Click **Save**.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="11806-191">移至 [LinkedIn 系統管理員設定] 區段。</span><span class="sxs-lookup"><span data-stu-id="11806-191">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="11806-192">按一下 [上傳 XML 檔案] 選項，將您剛剛從 Azure 入口網站下載的 XML 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="11806-192">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="11806-194">按一下 [開啟] 以啟用 SSO。</span><span class="sxs-lookup"><span data-stu-id="11806-194">Click **On** to enable SSO.</span></span> <span data-ttu-id="11806-195">SSO 狀態將會從 [未連線] 變更為 [已連線]</span><span class="sxs-lookup"><span data-stu-id="11806-195">SSO status will change from **Not Connected** to **Connected**</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11806-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="11806-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="11806-198">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="11806-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="11806-200">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="11806-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="11806-201">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="11806-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="11806-203">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="11806-203">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="11806-205">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="11806-205">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="11806-207">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="11806-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11806-209">a.</span><span class="sxs-lookup"><span data-stu-id="11806-209">a.</span></span> <span data-ttu-id="11806-210">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="11806-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11806-211">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="11806-211">b.</span></span> <span data-ttu-id="11806-212">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="11806-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11806-213">c.</span><span class="sxs-lookup"><span data-stu-id="11806-213">c.</span></span> <span data-ttu-id="11806-214">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="11806-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="11806-215">d.</span><span class="sxs-lookup"><span data-stu-id="11806-215">d.</span></span> <span data-ttu-id="11806-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="11806-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="11806-217">建立 LinkedIn Elevate 測試使用者</span><span class="sxs-lookup"><span data-stu-id="11806-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="11806-218">Linked Elevate 應用程式僅在使用者佈建時支援，驗證之後，會在應用程式中自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="11806-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="11806-219">在 LinkedIn Elevate 入口網站的系統管理設定頁面上，將 [自動指派授權] 切換為作用中，以在佈建時啟用，這個動作也會將授權指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="11806-219">On the admin settings page on the LinkedIn Elevate portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>

   ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="11806-221">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="11806-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="11806-222">在本節中，您會將 LinkedIn Elevate 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11806-222">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Elevate.</span></span>

![指派使用者][200] 

<span data-ttu-id="11806-224">**若要將 Britta Simon 指派給 LinkedIn Elevate，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="11806-224">**To assign Britta Simon to LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="11806-225">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="11806-225">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="11806-227">在應用程式清單中，選取 [LinkedIn Elevate]。</span><span class="sxs-lookup"><span data-stu-id="11806-227">In the applications list, select **LinkedIn Elevate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="11806-229">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="11806-229">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="11806-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11806-231">Click **Add** button.</span></span> <span data-ttu-id="11806-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="11806-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="11806-234">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="11806-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="11806-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11806-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11806-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11806-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="11806-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="11806-237">Testing single sign-on</span></span>

<span data-ttu-id="11806-238">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="11806-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="11806-239">當您在「存取面板」中按一下 LinkedIn Elevate 圖格時，您應該會進入 Azure 登入頁面；成功登入之後，您應該會進入 LinkedIn Elevate 應用程式。</span><span class="sxs-lookup"><span data-stu-id="11806-239">When you click the LinkedIn Elevate tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11806-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="11806-240">Additional resources</span></span>

* [<span data-ttu-id="11806-241">教學課程︰以 Azure Active Directory 設定自動使用者佈建的 LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="11806-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="11806-242">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="11806-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11806-243">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="11806-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


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
