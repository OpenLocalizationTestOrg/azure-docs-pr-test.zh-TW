---
title: "教學課程：Azure Active Directory 與 Pluralsight 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Pluralsight 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 62429643a108665544e42001d264046b5db1ec97
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="7302e-103">教學課程：Azure Active Directory 與 Pluralsight 整合</span><span class="sxs-lookup"><span data-stu-id="7302e-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="7302e-104">在本教學課程中，您會了解如何整合 Pluralsight 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7302e-104">In this tutorial, you learn how to integrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7302e-105">Pluralsight 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7302e-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7302e-106">您可以在 Azure AD 中控制可存取 Pluralsight 的人員</span><span class="sxs-lookup"><span data-stu-id="7302e-106">You can control in Azure AD who has access to Pluralsight</span></span>
- <span data-ttu-id="7302e-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Pluralsight (單一登入)</span><span class="sxs-lookup"><span data-stu-id="7302e-107">You can enable your users to automatically get signed-on to Pluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7302e-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="7302e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7302e-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7302e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7302e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7302e-110">Prerequisites</span></span>

<span data-ttu-id="7302e-111">若要設定與 Pluralsight 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7302e-111">To configure Azure AD integration with Pluralsight, you need the following items:</span></span>

- <span data-ttu-id="7302e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7302e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7302e-113">已啟用 Pluralsight 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7302e-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7302e-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7302e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7302e-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7302e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7302e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7302e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7302e-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7302e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7302e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7302e-118">Scenario description</span></span>
<span data-ttu-id="7302e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7302e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7302e-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7302e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7302e-121">從資源庫新增 Pluralsight</span><span class="sxs-lookup"><span data-stu-id="7302e-121">Adding Pluralsight from the gallery</span></span>
2. <span data-ttu-id="7302e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7302e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-the-gallery"></a><span data-ttu-id="7302e-123">從資源庫新增 Pluralsight</span><span class="sxs-lookup"><span data-stu-id="7302e-123">Adding Pluralsight from the gallery</span></span>
<span data-ttu-id="7302e-124">若要設定 Pluralsight 與 Azure AD 整合，您需要從資源庫將 Pluralsight 加入到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7302e-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7302e-125">**若要從資源庫加入 Pluralsight，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7302e-125">**To add Pluralsight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7302e-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7302e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7302e-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7302e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7302e-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7302e-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7302e-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7302e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7302e-133">在搜尋方塊中，輸入 **Pluralsight**。</span><span class="sxs-lookup"><span data-stu-id="7302e-133">In the search box, type **Pluralsight**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="7302e-135">在結果窗格中，選取 [Pluralsight]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7302e-135">In the results panel, select **Pluralsight**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7302e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7302e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7302e-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Pluralsight 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7302e-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7302e-139">若要讓單一登入運作，Azure AD 必須知道 Pluralsight 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7302e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pluralsight is to a user in Azure AD.</span></span> <span data-ttu-id="7302e-140">換句話說，必須建立 Azure AD 使用者和 Pluralsight 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7302e-140">In other words, a link relationship between an Azure AD user and the related user in Pluralsight needs to be established.</span></span>

<span data-ttu-id="7302e-141">在 Pluralsight 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7302e-141">In Pluralsight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7302e-142">若要設定及測試對 Pluralsight 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7302e-142">To configure and test Azure AD single sign-on with Pluralsight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7302e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7302e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7302e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7302e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7302e-145">**[建立 Pluralsight 測試使用者](#creating-a-pluralsight-test-user)** - 使 Pluralsight 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="7302e-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7302e-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7302e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7302e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7302e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7302e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7302e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7302e-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Pluralsight 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7302e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="7302e-150">**若要設定與 Pluralsight 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7302e-150">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="7302e-151">在 Azure 入口網站的 [Pluralsight] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7302e-151">In the Azure portal, on the **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7302e-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7302e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="7302e-155">在 [Pluralsight 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7302e-155">On the **Pluralsight Domain and URLs** section, perform the following:</span></span>

    ![設定單一登入](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="7302e-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="7302e-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7302e-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="7302e-158">This value is not real.</span></span> <span data-ttu-id="7302e-159">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="7302e-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="7302e-160">請連絡 [Pluralsight 客戶支援小組](mailto:support@pluralsight.com)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="7302e-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) to get this value.</span></span> 
 


4. <span data-ttu-id="7302e-161">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7302e-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="7302e-163">本節的目標是要在 Azure 入口網站中啟用 Azure AD 單一登入，並在 Pluralsight 應用程式中設定 SSO。</span><span class="sxs-lookup"><span data-stu-id="7302e-163">The objective of this section is to enable Azure AD single sign-on in the Azure portal and to configure SSO in the Pluralsight application.</span></span>

    <span data-ttu-id="7302e-164">Pluralsight 應用程式需要特定格式的 SAML 判斷提示，需要您加入自訂屬性對應到您的 SAML token 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="7302e-164">The Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="7302e-165">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="7302e-165">The following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="7302e-167">您也可以利用適當的值新增 **"Unique ID"** 屬性，例如 EmployeeID 和其他適合貴組織的值。</span><span class="sxs-lookup"><span data-stu-id="7302e-167">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="7302e-168">另請注意，這不是必要的屬性，但您可以新增它以識別唯一的使用者。</span><span class="sxs-lookup"><span data-stu-id="7302e-168">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span></span> 

6. <span data-ttu-id="7302e-169">若要加入必要的 [SAML Token 屬性] ，請對下表顯示的每一列執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7302e-169">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="7302e-170">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="7302e-170">Attribute Name</span></span> | <span data-ttu-id="7302e-171">屬性值</span><span class="sxs-lookup"><span data-stu-id="7302e-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="7302e-172">名字</span><span class="sxs-lookup"><span data-stu-id="7302e-172">First Name</span></span> |<span data-ttu-id="7302e-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7302e-173">user.givenname</span></span> |
   | <span data-ttu-id="7302e-174">姓氏</span><span class="sxs-lookup"><span data-stu-id="7302e-174">Last Name</span></span> |<span data-ttu-id="7302e-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="7302e-175">user.surname</span></span> |
   | <span data-ttu-id="7302e-176">電子郵件</span><span class="sxs-lookup"><span data-stu-id="7302e-176">Email</span></span> |<span data-ttu-id="7302e-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="7302e-177">user.mail</span></span> |
   
   <span data-ttu-id="7302e-178">a.</span><span class="sxs-lookup"><span data-stu-id="7302e-178">a.</span></span> <span data-ttu-id="7302e-179">按一下 [新增使用者屬性] 來開啟 [新增使用者屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7302e-179">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
    
     ![設定單一登入](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="7302e-181">b.</span><span class="sxs-lookup"><span data-stu-id="7302e-181">b.</span></span> <span data-ttu-id="7302e-182">在 [屬性名稱]  文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="7302e-182">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
  
   <span data-ttu-id="7302e-183">c.</span><span class="sxs-lookup"><span data-stu-id="7302e-183">c.</span></span> <span data-ttu-id="7302e-184">在 [屬性值]  清單中，選取該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="7302e-184">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
  
   <span data-ttu-id="7302e-185">d.</span><span class="sxs-lookup"><span data-stu-id="7302e-185">d.</span></span> <span data-ttu-id="7302e-186">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7302e-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="7302e-187">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7302e-187">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7302e-189">若要為您的應用程式設定 SSO，請連絡 [Pluralsight 專業服務](mailTo:professionalservices@pluralsight.com) 小組，並提供下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="7302e-189">To get SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="7302e-190">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7302e-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7302e-191">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7302e-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7302e-192">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7302e-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7302e-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7302e-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="7302e-194">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7302e-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7302e-196">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7302e-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7302e-197">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7302e-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7302e-199">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="7302e-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7302e-201">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7302e-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7302e-203">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7302e-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7302e-205">a.</span><span class="sxs-lookup"><span data-stu-id="7302e-205">a.</span></span> <span data-ttu-id="7302e-206">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7302e-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7302e-207">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7302e-207">b.</span></span> <span data-ttu-id="7302e-208">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7302e-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7302e-209">c.</span><span class="sxs-lookup"><span data-stu-id="7302e-209">c.</span></span> <span data-ttu-id="7302e-210">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="7302e-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7302e-211">d.</span><span class="sxs-lookup"><span data-stu-id="7302e-211">d.</span></span> <span data-ttu-id="7302e-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7302e-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="7302e-213">建立 Pluralsight 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7302e-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="7302e-214">本節目標是在 Pluralsight 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="7302e-214">The objective of this section is to create a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="7302e-215">請與 [Pluralsight 客戶支援小組](mailto:support@pluralsight.com)合作，在 Pluralsight 帳戶中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="7302e-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) to add the users in the Pluralsight account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7302e-216">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7302e-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7302e-217">在本節中，您會將 Pluralsight 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7302e-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pluralsight.</span></span>

![指派使用者][200] 

<span data-ttu-id="7302e-219">**若要將 Britta Simon 指派到 Pluralsight，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="7302e-219">**To assign Britta Simon to Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="7302e-220">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7302e-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7302e-222">在應用程式清單中，選取 [Pluralsight] 。</span><span class="sxs-lookup"><span data-stu-id="7302e-222">In the applications list, select **Pluralsight**.</span></span>

    ![設定單一登入](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="7302e-224">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7302e-224">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7302e-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7302e-226">Click **Add** button.</span></span> <span data-ttu-id="7302e-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7302e-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7302e-229">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7302e-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7302e-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7302e-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7302e-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7302e-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7302e-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7302e-232">Testing single sign-on</span></span>

<span data-ttu-id="7302e-233">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="7302e-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7302e-234">當您在存取面板中按一下 Pluralsight 圖格時，應該會自動登入您的 Pluralsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7302e-234">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span></span> <span data-ttu-id="7302e-235">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="7302e-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7302e-236">其他資源</span><span class="sxs-lookup"><span data-stu-id="7302e-236">Additional resources</span></span>

* [<span data-ttu-id="7302e-237">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7302e-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7302e-238">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7302e-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

