---
title: "教學課程：Azure Active Directory 與 LinkedIn Lookup 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 LinkedIn Lookup 之間的單一登入。"
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
ms.openlocfilehash: e296431866a8611b30e72f286884890adf0f7e50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="182d0-103">教學課程：Azure Active Directory 與 LinkedIn Lookup 整合</span><span class="sxs-lookup"><span data-stu-id="182d0-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="182d0-104">在本教學課程中，您將了解如何將 LinkedIn Lookup 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="182d0-104">In this tutorial, you learn how to integrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="182d0-105">LinkedIn Lookup 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="182d0-105">Integrating LinkedIn Lookup with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="182d0-106">您可以在 Azure AD 中控制可存取 LinkedIn Lookup 的人員</span><span class="sxs-lookup"><span data-stu-id="182d0-106">You can control in Azure AD who has access to LinkedIn Lookup</span></span>
- <span data-ttu-id="182d0-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 LinkedIn Lookup (單一登入)</span><span class="sxs-lookup"><span data-stu-id="182d0-107">You can enable your users to automatically get signed-on to LinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="182d0-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="182d0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="182d0-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="182d0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="182d0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="182d0-110">Prerequisites</span></span>

<span data-ttu-id="182d0-111">如要設定 Azure AD 與 LinkedIn Lookup 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="182d0-111">To configure Azure AD integration with LinkedIn Lookup, you need the following items:</span></span>

- <span data-ttu-id="182d0-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="182d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="182d0-113">已啟用 LinkedIn Lookup 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="182d0-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="182d0-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="182d0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="182d0-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="182d0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="182d0-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="182d0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="182d0-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="182d0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="182d0-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="182d0-118">Scenario description</span></span>
<span data-ttu-id="182d0-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="182d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="182d0-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="182d0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="182d0-121">從資源庫新增 LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="182d0-121">Adding LinkedIn Lookup from the gallery</span></span>
2. <span data-ttu-id="182d0-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="182d0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-the-gallery"></a><span data-ttu-id="182d0-123">從資源庫新增 LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="182d0-123">Adding LinkedIn Lookup from the gallery</span></span>
<span data-ttu-id="182d0-124">如要設定將 LinkedIn Lookup 整合到 Azure AD 中，您需要從資源庫將 LinkedIn Lookup 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="182d0-124">To configure the integration of LinkedIn Lookup into Azure AD, you need to add LinkedIn Lookup from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="182d0-125">**若要從資源庫新增 LinkedIn Lookup，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="182d0-125">**To add LinkedIn Lookup from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="182d0-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="182d0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="182d0-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="182d0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="182d0-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="182d0-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="182d0-131">按一下對話方塊頂端的 [新應用程式] 按鈕來新增新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="182d0-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="182d0-133">在搜尋方塊中，輸入 **LinkedIn Lookup**。</span><span class="sxs-lookup"><span data-stu-id="182d0-133">In the search box, type **LinkedIn Lookup**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="182d0-135">在結果窗格中，選取 [LinkedIn Lookup]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="182d0-135">In the results panel, select **LinkedIn Lookup**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="182d0-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="182d0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="182d0-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 LinkedIn Lookup 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="182d0-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="182d0-139">若要讓單一登入能夠運作，Azure AD 必須知道 LinkedIn Lookup 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="182d0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Lookup is to a user in Azure AD.</span></span> <span data-ttu-id="182d0-140">換句話說，必須在 Azure AD 使用者和 LinkedIn Lookup 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="182d0-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Lookup needs to be established.</span></span>

<span data-ttu-id="182d0-141">建立此連結關聯性的方法，是將 Azure AD 中**使用者名稱**的值，指派為 LinkedIn Lookup 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="182d0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="182d0-142">若要設定及測試與 LinkedIn Lookup 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="182d0-142">To configure and test Azure AD single sign-on with LinkedIn Lookup, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="182d0-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="182d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="182d0-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="182d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="182d0-145">**[建立 LinkedIn Lookup 測試使用者](#creating-an-linkedin-lookup-test-user)** - 使 LinkedIn Lookup 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="182d0-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - to have a counterpart of Britta Simon in LinkedIn Lookup that is linked to the Azure AD representation.</span></span>
4. <span data-ttu-id="182d0-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="182d0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="182d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="182d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="182d0-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="182d0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="182d0-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 LinkedIn Lookup 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="182d0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="182d0-150">**如要設定搭配 LinkedIn Lookup 的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="182d0-150">**To configure Azure AD single sign-on with LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="182d0-151">在 Azure 入口網站的 [LinkedIn Lookup] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="182d0-151">In the Azure portal, on the **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="182d0-153">在 [單一登入] 對話方塊的 [模式] 中選取 [SAML 型登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="182d0-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="182d0-155">在不同的網頁瀏覽器視窗中，以管理員身分登入您的  網站。</span><span class="sxs-lookup"><span data-stu-id="182d0-155">In a different web browser window, sign-on to your **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="182d0-156">在 [帳戶中心] 中，按一下 [設定] 底下的 [全域設定]。</span><span class="sxs-lookup"><span data-stu-id="182d0-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="182d0-157">此外，從下拉式清單選取 [查詢]。</span><span class="sxs-lookup"><span data-stu-id="182d0-157">Also, select **Lookup** from the dropdown list.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="182d0-159">按一下 [或按一下這裡以從表單載入和複製個別欄位]，並複製 [實體識別碼] 和 [判斷提示取用者存取 (ACS) URL]</span><span class="sxs-lookup"><span data-stu-id="182d0-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="182d0-161">如果您想要在 [IDP 起始] 模式下設定應用程式，請在 Azure 入口網站的 [LinkedIn Lookup 網域和 URL] 區段下方執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="182d0-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="182d0-163">a.</span><span class="sxs-lookup"><span data-stu-id="182d0-163">a.</span></span> <span data-ttu-id="182d0-164">在 [識別碼] 文字方塊中，輸入從 LinkedIn 入口網站複製的 [實體 ID]</span><span class="sxs-lookup"><span data-stu-id="182d0-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="182d0-165">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="182d0-165">b.</span></span> <span data-ttu-id="182d0-166">在 [回覆 URL] 文字方塊中，輸入從 LinkedIn 入口網站複製的 [判斷提示取用者存取 (ACS) URL]</span><span class="sxs-lookup"><span data-stu-id="182d0-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="182d0-167">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]：</span><span class="sxs-lookup"><span data-stu-id="182d0-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="182d0-169">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="182d0-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="182d0-170">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="182d0-170">This is not real value.</span></span> <span data-ttu-id="182d0-171">使用者必須以實際的登入 URL 將這些值更新。</span><span class="sxs-lookup"><span data-stu-id="182d0-171">The user has to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="182d0-172">請連絡 [LinkedIn Lookup 用戶端支援小組](https://business.LinkedIn.com/lookup)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="182d0-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) to get this value.</span></span>

8. <span data-ttu-id="182d0-173">您的 **LinkedIn Lookup** 應用程式會預期要有特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="182d0-173">Your **LinkedIn Lookup** application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="182d0-174">使用者必須將自訂屬性對應新增至 SAML 權杖屬性設定。</span><span class="sxs-lookup"><span data-stu-id="182d0-174">The user has to add custom attribute mappings to the SAML token attributes configuration.</span></span> <span data-ttu-id="182d0-175">下列螢幕擷取畫面顯示了一個範例。</span><span class="sxs-lookup"><span data-stu-id="182d0-175">The following screenshot shows an example.</span></span> <span data-ttu-id="182d0-176">[使用者識別碼] 的預設值是 **user.userprincipalname**，但是 LinkedIn Lookup 預期它是與使用者電子郵件地址對應的值。</span><span class="sxs-lookup"><span data-stu-id="182d0-176">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="182d0-177">您可以使用清單中的 **user.mail** 屬性，或者根據組織組態使用適當的屬性值。</span><span class="sxs-lookup"><span data-stu-id="182d0-177">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="182d0-179">在 [使用者屬性] 區段中，按一下 [檢視及編輯所有其他使用者屬性]，然後設定屬性。</span><span class="sxs-lookup"><span data-stu-id="182d0-179">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="182d0-180">使用者需要新增名稱為 **email**、**department**、**firstname** 和 **lastname** 的四個宣告，而且值必須分別與 **user.mail**、**user.department**、**user.givenname** 和 **user.surname** 對應</span><span class="sxs-lookup"><span data-stu-id="182d0-180">The user needs to add four claims named **email**,  **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="182d0-181">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="182d0-181">Attribute Name</span></span> | <span data-ttu-id="182d0-182">屬性值</span><span class="sxs-lookup"><span data-stu-id="182d0-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="182d0-183">電子郵件</span><span class="sxs-lookup"><span data-stu-id="182d0-183">email</span></span>| <span data-ttu-id="182d0-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="182d0-184">user.mail</span></span> |    
    | <span data-ttu-id="182d0-185">department</span><span class="sxs-lookup"><span data-stu-id="182d0-185">department</span></span>| <span data-ttu-id="182d0-186">user.department</span><span class="sxs-lookup"><span data-stu-id="182d0-186">user.department</span></span> |
    | <span data-ttu-id="182d0-187">firstname</span><span class="sxs-lookup"><span data-stu-id="182d0-187">firstname</span></span>| <span data-ttu-id="182d0-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="182d0-188">user.givenname</span></span> |
    | <span data-ttu-id="182d0-189">lastname</span><span class="sxs-lookup"><span data-stu-id="182d0-189">lastname</span></span>| <span data-ttu-id="182d0-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="182d0-190">user.surname</span></span> |

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="182d0-192">a.</span><span class="sxs-lookup"><span data-stu-id="182d0-192">a.</span></span> <span data-ttu-id="182d0-193">按一下 [新增屬性] 以開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="182d0-193">Click **Add Attribute** to open the **Add Attribute** dialog.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="182d0-196">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="182d0-196">b.</span></span> <span data-ttu-id="182d0-197">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="182d0-197">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="182d0-198">c.</span><span class="sxs-lookup"><span data-stu-id="182d0-198">c.</span></span> <span data-ttu-id="182d0-199">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="182d0-199">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="182d0-200">d.</span><span class="sxs-lookup"><span data-stu-id="182d0-200">d.</span></span> <span data-ttu-id="182d0-201">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="182d0-201">Click **Ok**</span></span>

10. <span data-ttu-id="182d0-202">針對 **name** 屬性執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="182d0-202">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="182d0-203">a.</span><span class="sxs-lookup"><span data-stu-id="182d0-203">a.</span></span> <span data-ttu-id="182d0-204">按一下該屬性，以開啟 [編輯屬性] 視窗。</span><span class="sxs-lookup"><span data-stu-id="182d0-204">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="182d0-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="182d0-206">b.</span></span> <span data-ttu-id="182d0-207">刪除**命名空間**中的 URL 值。</span><span class="sxs-lookup"><span data-stu-id="182d0-207">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="182d0-208">c.</span><span class="sxs-lookup"><span data-stu-id="182d0-208">c.</span></span> <span data-ttu-id="182d0-209">按一下 [確定] 以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="182d0-209">Click **Ok** to save the setting.</span></span>

10. <span data-ttu-id="182d0-210">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="182d0-210">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="182d0-212">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="182d0-212">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="182d0-214">移至 [LinkedIn 系統管理員設定] 區段。</span><span class="sxs-lookup"><span data-stu-id="182d0-214">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="182d0-215">按一下 [上傳 XML 檔案] 選項，將您從 Azure 入口網站下載的 XML 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="182d0-215">Upload the XML file you downloaded from the Azure portal by clicking the **Upload XML file** option.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="182d0-217">按一下 [開啟] 以啟用 SSO。</span><span class="sxs-lookup"><span data-stu-id="182d0-217">Click **On** to enable SSO.</span></span> <span data-ttu-id="182d0-218">SSO 狀態會從 [未連線] 變更為 [已連線]</span><span class="sxs-lookup"><span data-stu-id="182d0-218">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="182d0-220">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="182d0-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="182d0-221">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="182d0-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="182d0-222">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="182d0-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="182d0-223">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="182d0-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="182d0-224">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="182d0-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="182d0-226">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="182d0-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="182d0-227">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="182d0-227">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="182d0-229">移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="182d0-229">Go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="182d0-231">按一下 [新增] 將 [使用者] 對話方塊開啟。</span><span class="sxs-lookup"><span data-stu-id="182d0-231">Click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="182d0-233">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="182d0-233">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="182d0-235">a.</span><span class="sxs-lookup"><span data-stu-id="182d0-235">a.</span></span> <span data-ttu-id="182d0-236">在 [名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="182d0-236">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="182d0-237">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="182d0-237">b.</span></span> <span data-ttu-id="182d0-238">在 [使用者名稱] 文字方塊中，輸入 Britta Simon 的「電子郵件地址」。</span><span class="sxs-lookup"><span data-stu-id="182d0-238">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="182d0-239">c.</span><span class="sxs-lookup"><span data-stu-id="182d0-239">c.</span></span> <span data-ttu-id="182d0-240">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="182d0-240">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="182d0-241">d.</span><span class="sxs-lookup"><span data-stu-id="182d0-241">d.</span></span> <span data-ttu-id="182d0-242">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="182d0-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="182d0-243">建立 LinkedIn Lookup 測試使用者</span><span class="sxs-lookup"><span data-stu-id="182d0-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="182d0-244">LinkedIn Lookup 應用程式支援及時 (JIT) 使用者佈建，而在驗證之後，應用程式會自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="182d0-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="182d0-245">啟用 [自動指派授權] 以指派授權給使用者。</span><span class="sxs-lookup"><span data-stu-id="182d0-245">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="182d0-247">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="182d0-247">Assigning the Azure AD test user</span></span>

<span data-ttu-id="182d0-248">在本節中，您會將 LinkedIn Lookup 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="182d0-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Lookup.</span></span>

![指派使用者][200] 

<span data-ttu-id="182d0-250">**若要將 Britta Simon 指派給 LinkedIn Lookup，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="182d0-250">**To assign Britta Simon to LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="182d0-251">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="182d0-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="182d0-253">在應用程式清單中，選取 [LinkedIn Lookup]。</span><span class="sxs-lookup"><span data-stu-id="182d0-253">In the applications list, select **LinkedIn Lookup**.</span></span>

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="182d0-255">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="182d0-255">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="182d0-257">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="182d0-257">Click **Add** button.</span></span> <span data-ttu-id="182d0-258">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="182d0-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="182d0-260">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="182d0-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="182d0-261">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="182d0-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="182d0-262">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="182d0-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="182d0-263">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="182d0-263">Testing single sign-on</span></span>

<span data-ttu-id="182d0-264">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="182d0-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="182d0-265">當您按一下存取面板中的 [LinkedIn Lookup] 圖格時，系統應該會將您重新導向至組織的頁面，您必須在其中提供您個人的 LinkedIn 帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="182d0-265">When you click the LinkedIn Lookup tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="182d0-266">它會連結您的個人帳戶與您的 LinkedIn 商務帳戶。</span><span class="sxs-lookup"><span data-stu-id="182d0-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="182d0-267">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="182d0-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="182d0-268">其他資源</span><span class="sxs-lookup"><span data-stu-id="182d0-268">Additional resources</span></span>

* [<span data-ttu-id="182d0-269">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="182d0-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="182d0-270">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="182d0-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

