---
title: "教學課程：Azure Active Directory 與 SAP Business Object Cloud 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SAP Business Object Cloud 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: 6d517c5e302ac36e5bba2053998c75f8f4d42683
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="180f0-103">教學課程：Azure Active Directory 與 SAP Business Object Cloud 整合</span><span class="sxs-lookup"><span data-stu-id="180f0-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="180f0-104">在本教學課程中，您將了解如何整合 SAP Business Object Cloud 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="180f0-104">In this tutorial, you learn how to integrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="180f0-105">將 SAP Business Object Cloud 與 Azure AD 整合時，您會獲得下列優點：</span><span class="sxs-lookup"><span data-stu-id="180f0-105">You get the following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="180f0-106">您可以在 Azure AD 中控制可存取 SAP Business Object Cloud 的人員。</span><span class="sxs-lookup"><span data-stu-id="180f0-106">In Azure AD, you can control who has access to SAP Business Object Cloud.</span></span>
- <span data-ttu-id="180f0-107">您可以使用單一登入和使用者的 Azure AD 帳戶，將您的使用者自動登入 SAP Business Object Cloud。</span><span class="sxs-lookup"><span data-stu-id="180f0-107">You can automatically sign in your users to SAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="180f0-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="180f0-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="180f0-109">若要深入了解軟體即服務 (SaaS) 應用程式與 Azure AD 的整合，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="180f0-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="180f0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="180f0-110">Prerequisites</span></span>

<span data-ttu-id="180f0-111">若要進行 Azure AD 與 SAP Business Object Cloud 整合的設定，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="180f0-111">To set up Azure AD integration with SAP Business Object Cloud, you need the following items:</span></span>

- <span data-ttu-id="180f0-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="180f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="180f0-113">已開啟單一登入的 SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="180f0-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="180f0-114">若您要測試本教學課程中的步驟，不建議您在生產環境中進行測試。</span><span class="sxs-lookup"><span data-stu-id="180f0-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="180f0-115">在本教學課程中測試步驟的建議：</span><span class="sxs-lookup"><span data-stu-id="180f0-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="180f0-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="180f0-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="180f0-117">如果您沒有 Azure AD 試用環境，可以[取得一個月的免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="180f0-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="180f0-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="180f0-118">Scenario description</span></span>
<span data-ttu-id="180f0-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="180f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="180f0-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="180f0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="180f0-121">從資源庫新增 SAP Business Object Cloud。</span><span class="sxs-lookup"><span data-stu-id="180f0-121">Add SAP Business Object Cloud from the gallery.</span></span>
2. <span data-ttu-id="180f0-122">設定和測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="180f0-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-the-gallery"></a><span data-ttu-id="180f0-123">從資源庫新增 SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="180f0-123">Add SAP Business Object Cloud from the gallery</span></span>
<span data-ttu-id="180f0-124">若要進行 SAP Business Object Cloud 與 Azure AD 整合的設定，請在資源庫中將 SAP Business Object Cloud 新增至受管理 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="180f0-124">To set up the integration of SAP Business Object Cloud with Azure AD, in the gallery, add SAP Business Object Cloud to your list of managed SaaS apps.</span></span>

<span data-ttu-id="180f0-125">若要從資源庫新增 SAP Business Object Cloud：</span><span class="sxs-lookup"><span data-stu-id="180f0-125">To add SAP Business Object Cloud from the gallery:</span></span>

1. <span data-ttu-id="180f0-126">在 [Azure 入口網站](https://portal.azure.com)的左側功能表中，選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="180f0-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="180f0-128">選取 [企業應用程式]，然後選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="180f0-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![[企業應用程式] 頁面][2]
    
3. <span data-ttu-id="180f0-130">若要新增新的應用程式，請選取 [新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="180f0-130">To add a new application, select **New application**.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="180f0-132">在搜尋方塊中，輸入 **SAP Business Object Cloud**。</span><span class="sxs-lookup"><span data-stu-id="180f0-132">In the search box, enter **SAP Business Object Cloud**.</span></span>

    ![搜尋方塊](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="180f0-134">在結果面板中，選取 [SAP Business Object Cloud]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="180f0-134">In the results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![結果清單中的 SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="180f0-136">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="180f0-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="180f0-137">在本節中，您將以名為 Britta Simon 的測試使用者身分，設定及測試與 SAP Business Object Cloud 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="180f0-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="180f0-138">為使單一登入運作，Azure AD 必須知道 SAP Business Object Cloud 中互相對應的 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="180f0-138">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="180f0-139">必須在 Azure AD 使用者與 SAP Business Object Cloud 的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="180f0-139">A link relationship between an Azure AD user and the related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="180f0-140">若要建立連結關聯性，在 SAP Business Object Cloud 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="180f0-140">To establish the link relationship, in SAP Business Object Cloud, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="180f0-141">若要設定及測試與 SAP Business Object Cloud 搭配運作的 Azure AD 單一登入，請完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="180f0-141">To configure and test Azure AD single sign-on with SAP Business Object Cloud, complete the following tasks:</span></span>

1. <span data-ttu-id="180f0-142">[設定 Azure AD 單一登入](#set-up-azure-ad-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="180f0-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="180f0-143">設定要使用這項功能的使用者。</span><span class="sxs-lookup"><span data-stu-id="180f0-143">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="180f0-144">[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)。</span><span class="sxs-lookup"><span data-stu-id="180f0-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="180f0-145">使用 Britta Simon 使用者來測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="180f0-145">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="180f0-146">[建立 SAP Business Object Cloud 測試使用者](#create-an-sap-business-object-cloud-test-user)。</span><span class="sxs-lookup"><span data-stu-id="180f0-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="180f0-147">在 SAP Business Object Cloud 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="180f0-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="180f0-148">[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)。</span><span class="sxs-lookup"><span data-stu-id="180f0-148">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="180f0-149">將 Britta Simon 設定為使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="180f0-149">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="180f0-150">[測試單一登入](#test-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="180f0-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="180f0-151">驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="180f0-151">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="180f0-152">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="180f0-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="180f0-153">在本節中，您會在 Azure 入口網站開啟 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="180f0-153">In this section, you turn on Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="180f0-154">然後，您要在 SAP Business Object Cloud 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="180f0-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="180f0-155">若要使用 SAP Business Object Cloud 設定 Azure AD 單一登入：</span><span class="sxs-lookup"><span data-stu-id="180f0-155">To set up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="180f0-156">在 Azure 入口網站的 [SAP Business Object Cloud] 應用程式整合頁面上，選取 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="180f0-156">In the Azure portal, on the **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![選取 [單一登入]][4]

2. <span data-ttu-id="180f0-158">在 [單一登入] 頁面上，選取 [SAML 登入] 作為 [模式]。</span><span class="sxs-lookup"><span data-stu-id="180f0-158">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![選取 SAML 登入](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="180f0-160">在 [SAP Business Object Cloud 網域及 URL] 下，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="180f0-160">Under **SAP Business Object Cloud Domain and URLs**, complete the following steps:</span></span>

    1. <span data-ttu-id="180f0-161">在 [登入 URL] 方塊中，輸入具有下列模式的 URL：</span><span class="sxs-lookup"><span data-stu-id="180f0-161">In the **Sign-on URL** box, enter a URL that has the following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="180f0-162">在 [識別碼] 方塊中，輸入具有下列模式的 URL：</span><span class="sxs-lookup"><span data-stu-id="180f0-162">In the **Identifier** box, enter a URL that has the following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![SAP Business Object Cloud 網域和 URL 頁面的 URL](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="180f0-164">這些 URL 中的值僅供示範。</span><span class="sxs-lookup"><span data-stu-id="180f0-164">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="180f0-165">使用實際的「登入 URL」及「識別碼 URL」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="180f0-165">Update the values with the actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="180f0-166">若要取得登入 URL，請連絡 [SAP Business Object Cloud 用戶端支援小組](https://www.sap.com/product/analytics/cloud-analytics.support.html)。</span><span class="sxs-lookup"><span data-stu-id="180f0-166">To get the sign-on URL, contact the [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="180f0-167">您可以從系統管理員主控台下載 SAP Business Object Cloud 中繼資料，以取得識別項 URL。</span><span class="sxs-lookup"><span data-stu-id="180f0-167">You can get the identifier URL by downloading the SAP Business Object Cloud metadata from the admin console.</span></span> <span data-ttu-id="180f0-168">稍後在本教學課程中會加以說明。</span><span class="sxs-lookup"><span data-stu-id="180f0-168">This is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="180f0-169">在 [SAML 簽章憑證] 下，選取 [中繼資料 XML]。</span><span class="sxs-lookup"><span data-stu-id="180f0-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="180f0-170">然後，將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="180f0-170">Then, save the metadata file on your computer.</span></span>

    ![選取 [中繼資料 XML]](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="180f0-172">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="180f0-172">Select **Save**.</span></span>

    ![選取 [儲存]](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="180f0-174">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 SAP Business Object Cloud 公司網站。</span><span class="sxs-lookup"><span data-stu-id="180f0-174">In a different web browser window, sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="180f0-175">選取 [功能表] > [系統] > [管理]。</span><span class="sxs-lookup"><span data-stu-id="180f0-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![依序選取 [功能表]、[系統] 和 [管理]](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="180f0-177">在 [安全性] 索引標籤上，選取 [編輯] \(畫筆) 圖示。</span><span class="sxs-lookup"><span data-stu-id="180f0-177">On the **Security** tab, select the **Edit** (pen) icon.</span></span>
    
    ![在 [安全性] 索引標籤上，選取 [編輯] 圖示](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="180f0-179">選取 [SAML 單一登入 (SSO)] 作為 [驗證方法]。</span><span class="sxs-lookup"><span data-stu-id="180f0-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![選取 [SAML 單一登入] 作為驗證方法](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="180f0-181">選取 [下載]，以下載服務提供者中繼資料 (步驟 1)。</span><span class="sxs-lookup"><span data-stu-id="180f0-181">To download the service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="180f0-182">在中繼資料檔案中，尋找並複製 **entityID** 值。</span><span class="sxs-lookup"><span data-stu-id="180f0-182">In the metadata file, find and copy the **entityID** value.</span></span> <span data-ttu-id="180f0-183">在 Azure 入口網站中，在 [SAP Business Object Cloud 網域和 URL] 下，將值貼入 [識別碼] 方塊。</span><span class="sxs-lookup"><span data-stu-id="180f0-183">In the Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste the value in the **Identifier** box.</span></span>

    ![複製並貼上 entityID 值](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="180f0-185">若要在您從 Azure 入口網站下載的檔案中上傳服務提供者中繼資料 (步驟 2)**，請在 [上傳識別提供者中繼資料]** 下，選取 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="180f0-185">To upload the service provider metadata (Step 2) in the file that you downloaded from the Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![在上傳識別提供者中繼資料下，選取 [上傳]](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="180f0-187">在 [使用者屬性值] 清單中，選取您需要用於實作的使用者屬性 (步驟 3)。</span><span class="sxs-lookup"><span data-stu-id="180f0-187">In the **User Attribute** list, select the user attribute (Step 3) that you want to use for your implementation.</span></span> <span data-ttu-id="180f0-188">此使用者屬性會對應到識別提供者。</span><span class="sxs-lookup"><span data-stu-id="180f0-188">This user attribute maps to the identity provider.</span></span> <span data-ttu-id="180f0-189">若要在使用者的頁面上輸入自訂屬性，請使用 [自訂 SAML 對應] 選項。</span><span class="sxs-lookup"><span data-stu-id="180f0-189">To enter a custom attribute on the user's page, use the **Custom SAML Mapping** option.</span></span> <span data-ttu-id="180f0-190">或者，您可以選取 [電子郵件] 或 [使用者識別碼]作為使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="180f0-190">Or, you can select either **Email** or **USER ID** as the user attribute.</span></span> <span data-ttu-id="180f0-191">在本範例中，我們選取 [電子郵件]，因為我們在 Azure 入口網站的 [使用者屬性] 區段中，使用 **userprincipalname** 屬性來對應使用者識別項宣告。</span><span class="sxs-lookup"><span data-stu-id="180f0-191">In our example, we selected **Email** because we mapped the user identifier claim with the **userprincipalname** attribute in the **User Attributes** section in the Azure portal.</span></span> <span data-ttu-id="180f0-192">這會提供唯一的使用者電子郵件，並傳送給每個成功 SAML 回應中的 SAP Business Object Cloud 應用程式。</span><span class="sxs-lookup"><span data-stu-id="180f0-192">This provides a unique user email, which is sent to the SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![選取使用者屬性](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="180f0-194">若要使用識別提供者 (步驟 4) 來驗證帳戶，請在 [登入認證 (電子郵件)] 方塊中，輸入使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="180f0-194">To verify the account with the identity provider (Step 4), in the **Login Credential (Email)** box, enter the user's email address.</span></span> <span data-ttu-id="180f0-195">然後，選取 [驗證帳戶]。</span><span class="sxs-lookup"><span data-stu-id="180f0-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="180f0-196">系統會將登入認證新增至使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="180f0-196">The system adds sign-in credentials to the user account.</span></span>

    ![輸入電子郵件，並選取 [驗證帳戶]](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="180f0-198">選取 [儲存] 圖示。</span><span class="sxs-lookup"><span data-stu-id="180f0-198">Select the **Save** icon.</span></span>

    ![[儲存] 圖示](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="180f0-200">當您設定應用程式時，在 [Azure 入口網站](https://portal.azure.com)中即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="180f0-200">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="180f0-201">選取 [Active Directory] > [企業應用程式] 新增此應用程式之後，選取 [單一登入] 索引標籤。您可以透過頁面底部的 [設定] 區段來存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="180f0-201">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="180f0-202">如需詳細資訊，請參閱 [Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)。</span><span class="sxs-lookup"><span data-stu-id="180f0-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="180f0-203">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="180f0-203">Create an Azure AD test user</span></span>
<span data-ttu-id="180f0-204">在本節中，您會在 Azure 入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="180f0-204">In this section, you create a test user named Britta Simon in the Azure portal.</span></span>

<span data-ttu-id="180f0-205">若要在 Azure AD 中建立測試使用者：</span><span class="sxs-lookup"><span data-stu-id="180f0-205">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="180f0-206">在 Azure 入口網站的左側功能表中，選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="180f0-206">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="180f0-208">若要顯示使用者清單，請選取 [使用者和群組]，然後選取 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="180f0-208">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="180f0-210">若要開啟 [使用者] 對話方塊，請選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="180f0-210">To open the **User** dialog box, select **Add**.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="180f0-212">在 [使用者] 對話方塊中，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="180f0-212">In the **User** dialog box, complete the following steps:</span></span>
 
    1. <span data-ttu-id="180f0-213">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="180f0-213">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="180f0-214">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="180f0-214">In the **User name** box, enter the email address of the user Britta Simon.</span></span>

    3. <span data-ttu-id="180f0-215">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="180f0-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="180f0-216">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="180f0-216">Select **Create**.</span></span>

        ![[使用者] 對話方塊](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![建立 Azure AD 使用者][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="180f0-219">建立 SAP Business Object Cloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="180f0-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="180f0-220">必須在 SAP Business Object Cloud 中佈建 Azure AD 使用者之後，他們才能登入 SAP Business Object Cloud。</span><span class="sxs-lookup"><span data-stu-id="180f0-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in to SAP Business Object Cloud.</span></span> <span data-ttu-id="180f0-221">在 SAP Business Object Cloud 中，必須以手動方式進行佈建。</span><span class="sxs-lookup"><span data-stu-id="180f0-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="180f0-222">若要佈建使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="180f0-222">To provision a user account:</span></span>

1. <span data-ttu-id="180f0-223">以系統管理員身分登入您的 SAP Business Object Cloud 公司網站。</span><span class="sxs-lookup"><span data-stu-id="180f0-223">Sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="180f0-224">選取 [功能表] > [安全性] > [使用者]。</span><span class="sxs-lookup"><span data-stu-id="180f0-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![新增員工](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="180f0-226">若要在 [使用者] 頁面上新增新的使用者詳細資料，請選取 [+]。</span><span class="sxs-lookup"><span data-stu-id="180f0-226">On the **Users** page, to add new user details, select **+**.</span></span> 

    ![新增使用者頁面](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="180f0-228">然後完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="180f0-228">Then, complete the following steps:</span></span>

    1. <span data-ttu-id="180f0-229">在 [使用者識別碼] 方塊中，輸入使用者的使用者識別碼，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="180f0-229">In the **USER ID** box, enter the user ID of the user, like **Britta**.</span></span>

    2. <span data-ttu-id="180f0-230">在 [名字] 方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="180f0-230">In the **FIRST NAME** box, enter the first name of the user, like **Britta**.</span></span>

    3. <span data-ttu-id="180f0-231">在 [姓氏] 方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="180f0-231">In the **LAST NAME** box, enter the last name of the user, like **Simon**.</span></span>

    4. <span data-ttu-id="180f0-232">在 [顯示名稱] 方塊中，輸入使用者的全名，例如 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="180f0-232">In the **DISPLAY NAME** box, enter the full name of the user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="180f0-233">在 [電子郵件] 方塊中，輸入使用者的電子郵件地址，例如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="180f0-233">In the **E-MAIL** box, enter the email address of the user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="180f0-234">在 [選取角色] 頁面上，選取適當的使用者角色，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="180f0-234">On the **Select Roles** page, select the appropriate role for the user, and then select **OK**.</span></span>

      ![選取角色](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="180f0-236">選取 [儲存] 圖示。</span><span class="sxs-lookup"><span data-stu-id="180f0-236">Select the **Save** icon.</span></span>    


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="180f0-237">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="180f0-237">Assign the Azure AD test user</span></span>

<span data-ttu-id="180f0-238">在本節中，您會將 SAP Business Object Cloud 的使用者帳戶存取權授與使用者 Britta Simon，讓她能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="180f0-238">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to SAP Business Object Cloud.</span></span>

<span data-ttu-id="180f0-239">若要將 Britta Simon 指派到 SAP Business Object Cloud：</span><span class="sxs-lookup"><span data-stu-id="180f0-239">To assign Britta Simon to SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="180f0-240">在 Azure 入口網站中，開啟應用程式檢視，然後移至目錄檢視。</span><span class="sxs-lookup"><span data-stu-id="180f0-240">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="180f0-241">選取 [企業應用程式]，然後選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="180f0-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="180f0-243">在應用程式清單中，選取 [SAP Business Object Cloud]。</span><span class="sxs-lookup"><span data-stu-id="180f0-243">In the applications list, select **SAP Business Object Cloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="180f0-245">在左側功能表中，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="180f0-245">In the left menu, select **Users and groups**.</span></span>

    ![選取 [使用者和群組]][202] 

4. <span data-ttu-id="180f0-247">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="180f0-247">Select **Add**.</span></span> <span data-ttu-id="180f0-248">然後在 [新增指派] 頁面上，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="180f0-248">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="180f0-250">在 [使用者和群組] 頁面上，選取使用者清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="180f0-250">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="180f0-251">在 [使用者和群組] 頁面上，選取 [選取]。</span><span class="sxs-lookup"><span data-stu-id="180f0-251">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="180f0-252">在 [新增指派] 頁面上，選取 [指派]。</span><span class="sxs-lookup"><span data-stu-id="180f0-252">On the **Add Assignment** page, select **Assign**.</span></span>

![指派使用者角色][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="180f0-254">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="180f0-254">Test single sign-on</span></span>

<span data-ttu-id="180f0-255">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="180f0-255">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="180f0-256">選取存取面板中的 [SAP Business Object Cloud] 圖格時，應會自動登入您的 SAP Business Object Cloud 應用程式。</span><span class="sxs-lookup"><span data-stu-id="180f0-256">When you select the SAP Business Object Cloud tile in the access panel, you should be automatically signed in to your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="180f0-257">如需存取面板的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="180f0-257">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="180f0-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="180f0-258">Additional resources</span></span>

* [<span data-ttu-id="180f0-259">如何整合 SaaS 應用程式與 Azure Active Directory 的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="180f0-259">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="180f0-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="180f0-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

