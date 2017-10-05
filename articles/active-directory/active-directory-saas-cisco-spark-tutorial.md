---
title: "教學課程：Azure Active Directory 與 Cisco Spark 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Cisco Spark 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: a0a221622afe1c801a331e2319f3a7ace3111dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="1bba6-103">教學課程：Azure Active Directory 與 Cisco Spark 整合</span><span class="sxs-lookup"><span data-stu-id="1bba6-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="1bba6-104">在本教學課程中，您會了解如何整合 Cisco Spark 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1bba6-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1bba6-105">將 Cisco Spark 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="1bba6-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1bba6-106">您可以在 Azure AD 中控制可存取 Cisco Spark 的人員</span><span class="sxs-lookup"><span data-stu-id="1bba6-106">You can control in Azure AD who has access to Cisco Spark</span></span>
- <span data-ttu-id="1bba6-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Cisco Spark (單一登入)</span><span class="sxs-lookup"><span data-stu-id="1bba6-107">You can enable your users to automatically get signed-on to Cisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1bba6-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="1bba6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1bba6-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1bba6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bba6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1bba6-110">Prerequisites</span></span>

<span data-ttu-id="1bba6-111">若要設定 Azure AD 與 Cisco Spark 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="1bba6-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span></span>

- <span data-ttu-id="1bba6-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1bba6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1bba6-113">已啟用 Cisco Spark 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1bba6-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1bba6-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1bba6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1bba6-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1bba6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1bba6-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1bba6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1bba6-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1bba6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1bba6-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1bba6-118">Scenario description</span></span>
<span data-ttu-id="1bba6-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bba6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1bba6-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="1bba6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1bba6-121">從資源庫新增 Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="1bba6-121">Adding Cisco Spark from the gallery</span></span>
2. <span data-ttu-id="1bba6-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1bba6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-the-gallery"></a><span data-ttu-id="1bba6-123">從資源庫新增 Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="1bba6-123">Adding Cisco Spark from the gallery</span></span>
<span data-ttu-id="1bba6-124">若要設定將 Cisco Spark 整合到 Azure AD 中，您需要從資源庫將 Cisco Spark 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="1bba6-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1bba6-125">**若要從資源庫新增 Cisco Spark，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1bba6-125">**To add Cisco Spark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1bba6-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1bba6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1bba6-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1bba6-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1bba6-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1bba6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1bba6-133">在搜尋方塊中，輸入 **Cisco Spark**。</span><span class="sxs-lookup"><span data-stu-id="1bba6-133">In the search box, type **Cisco Spark**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="1bba6-135">在結果窗格中，選取 [Cisco Spark]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bba6-135">In the results panel, select **Cisco Spark**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1bba6-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1bba6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1bba6-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Cisco Spark 設定和測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bba6-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1bba6-139">若要讓單一登入運作，Azure AD 必須知道 Cisco Spark 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="1bba6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span></span> <span data-ttu-id="1bba6-140">換句話說，必須在 Azure AD 使用者和 Cisco Spark 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1bba6-140">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span></span>

<span data-ttu-id="1bba6-141">在 Cisco Spark 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1bba6-141">In Cisco Spark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1bba6-142">若要設定和測試對 Cisco Spark 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1bba6-142">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1bba6-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="1bba6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1bba6-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bba6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1bba6-145">**[建立 Cisco Spark 測試使用者](#creating-a-cisco-spark-test-user)** - 使 Cisco Spark 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="1bba6-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1bba6-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bba6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1bba6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="1bba6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1bba6-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1bba6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1bba6-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Cisco Spark 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bba6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="1bba6-150">**若要設定與 Cisco Spark 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1bba6-150">**To configure Azure AD single sign-on with Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="1bba6-151">在 Azure 入口網站的 [Cisco Spark] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-151">In the Azure portal, on the **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1bba6-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bba6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="1bba6-155">在 [Cisco Spark 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1bba6-155">On the **Cisco Spark Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="1bba6-157">a.</span><span class="sxs-lookup"><span data-stu-id="1bba6-157">a.</span></span> <span data-ttu-id="1bba6-158">在 [登入 URL] 文字方塊中，將 URL 輸入為：`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="1bba6-158">In the **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="1bba6-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bba6-159">b.</span></span> <span data-ttu-id="1bba6-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="1bba6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1bba6-161">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="1bba6-161">This value is not real.</span></span> <span data-ttu-id="1bba6-162">請使用實際的「識別碼」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="1bba6-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="1bba6-163">請連絡 [Cisco Spark 用戶端支援小組](https://support.ciscospark.com/)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="1bba6-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) to get this value.</span></span> 
 
4. <span data-ttu-id="1bba6-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="1bba6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="1bba6-166">Cisco Spark 應用程式預期 SAML 判斷提示會包含特定屬性。</span><span class="sxs-lookup"><span data-stu-id="1bba6-166">Cisco Spark application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="1bba6-167">設定此應用程式的下列屬性。</span><span class="sxs-lookup"><span data-stu-id="1bba6-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="1bba6-168">您可以在應用程式整合頁面的 [使用者屬性] 區段中，管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="1bba6-168">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="1bba6-169">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="1bba6-169">The following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="1bba6-171">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1bba6-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="1bba6-172">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="1bba6-172">Attribute Name</span></span>  | <span data-ttu-id="1bba6-173">屬性值</span><span class="sxs-lookup"><span data-stu-id="1bba6-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="1bba6-174">UID</span><span class="sxs-lookup"><span data-stu-id="1bba6-174">uid</span></span>    | <span data-ttu-id="1bba6-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="1bba6-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="1bba6-176">a.</span><span class="sxs-lookup"><span data-stu-id="1bba6-176">a.</span></span> <span data-ttu-id="1bba6-177">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1bba6-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="1bba6-180">b.</span><span class="sxs-lookup"><span data-stu-id="1bba6-180">b.</span></span> <span data-ttu-id="1bba6-181">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="1bba6-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1bba6-182">c.</span><span class="sxs-lookup"><span data-stu-id="1bba6-182">c.</span></span> <span data-ttu-id="1bba6-183">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="1bba6-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1bba6-184">d.</span><span class="sxs-lookup"><span data-stu-id="1bba6-184">d.</span></span> <span data-ttu-id="1bba6-185">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1bba6-185">Click **Ok**.</span></span>

7. <span data-ttu-id="1bba6-186">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1bba6-186">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1bba6-188">使用完整系統管理員認證，登入 [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/)。</span><span class="sxs-lookup"><span data-stu-id="1bba6-188">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="1bba6-189">選取 [設定]，然後按一下 [驗證] 區段下方的 [修改]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-189">Select **Settings** and under the **Authentication** section, click **Modify**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="1bba6-191">選取 [整合協力廠商識別提供者 (進階)]，然後移至下一個畫面。</span><span class="sxs-lookup"><span data-stu-id="1bba6-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>

11. <span data-ttu-id="1bba6-192">在 [匯入 Idp 中繼資料] 頁面上，將 Azure AD 中繼資料檔案拖放到頁面，或使用檔案瀏覽器選項來找到並上傳 Azure AD 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="1bba6-192">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="1bba6-193">然後，選取 [需要中繼資料中憑證授權單位所簽署的憑證 (較安全)]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="1bba6-195">選取 [測試 SSO 連接]，並在新的瀏覽器索引標籤開啟時，透過登入向 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="1bba6-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="1bba6-196">返回 [Cisco Cloud Collaboration Management] 瀏覽器索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1bba6-196">Return to the **Cisco Cloud Collaboration Management** browser tab.</span></span> <span data-ttu-id="1bba6-197">如果測試成功，請選取 [這項測試成功。啟用單一登入] 選項，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-197">If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="1bba6-198">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="1bba6-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1bba6-199">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="1bba6-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1bba6-200">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1bba6-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1bba6-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1bba6-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="1bba6-202">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1bba6-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1bba6-204">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1bba6-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1bba6-205">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1bba6-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1bba6-207">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1bba6-209">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1bba6-211">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1bba6-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1bba6-213">a.</span><span class="sxs-lookup"><span data-stu-id="1bba6-213">a.</span></span> <span data-ttu-id="1bba6-214">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1bba6-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1bba6-215">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bba6-215">b.</span></span> <span data-ttu-id="1bba6-216">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="1bba6-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1bba6-217">c.</span><span class="sxs-lookup"><span data-stu-id="1bba6-217">c.</span></span> <span data-ttu-id="1bba6-218">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="1bba6-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1bba6-219">d.</span><span class="sxs-lookup"><span data-stu-id="1bba6-219">d.</span></span> <span data-ttu-id="1bba6-220">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1bba6-220">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="1bba6-221">建立 Cisco Spark 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1bba6-221">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="1bba6-222">在本節中，您要在 Cisco Spark 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="1bba6-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="1bba6-223">在本節中，您要在 Cisco Spark 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="1bba6-223">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="1bba6-224">使用完整系統管理員認證，移至 [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/)。</span><span class="sxs-lookup"><span data-stu-id="1bba6-224">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="1bba6-225">按一下 [使用者]，然後按一下 [管理使用者]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-225">Click **Users** and then **Manage Users**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="1bba6-227">在 [管理使用者] 視窗中，選取 [手動新增或修改使用者]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-227">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="1bba6-228">選取 [名稱和電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-228">Select **Names and Email address**.</span></span> <span data-ttu-id="1bba6-229">然後，如下填寫文字方塊︰</span><span class="sxs-lookup"><span data-stu-id="1bba6-229">Then, fill out the textbox as follows:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="1bba6-231">a.</span><span class="sxs-lookup"><span data-stu-id="1bba6-231">a.</span></span> <span data-ttu-id="1bba6-232">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="1bba6-232">In the **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="1bba6-233">b.</span><span class="sxs-lookup"><span data-stu-id="1bba6-233">b.</span></span> <span data-ttu-id="1bba6-234">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="1bba6-234">In the **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="1bba6-235">c.</span><span class="sxs-lookup"><span data-stu-id="1bba6-235">c.</span></span> <span data-ttu-id="1bba6-236">在 [電子郵件地址] 文字方塊中，輸入 **britta.simon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="1bba6-236">In the **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="1bba6-237">按一下加號以新增 Britta Simon。</span><span class="sxs-lookup"><span data-stu-id="1bba6-237">Click the plus sign to add Britta Simon.</span></span> <span data-ttu-id="1bba6-238">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1bba6-238">Then, click **Next**.</span></span>

6. <span data-ttu-id="1bba6-239">在 [新增使用者的服務] 視窗中，按一下 [儲存]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-239">In the **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1bba6-240">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1bba6-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1bba6-241">在本節中，您會將 Cisco Spark 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bba6-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Spark.</span></span>

![指派使用者][200] 

<span data-ttu-id="1bba6-243">**若要將 Britta Simon 指派到 Cisco Spark，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1bba6-243">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="1bba6-244">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1bba6-246">在應用程式清單中，選取 [Cisco Spark]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-246">In the applications list, select **Cisco Spark**.</span></span>

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="1bba6-248">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-248">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1bba6-250">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1bba6-250">Click **Add** button.</span></span> <span data-ttu-id="1bba6-251">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1bba6-253">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="1bba6-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1bba6-254">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1bba6-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1bba6-255">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1bba6-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1bba6-256">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1bba6-256">Testing single sign-on</span></span>

<span data-ttu-id="1bba6-257">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="1bba6-257">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1bba6-258">當您按一下存取面板中的 [Cisco Spark] 圖格時，應該會自動登入您的 Cisco Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bba6-258">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1bba6-259">其他資源</span><span class="sxs-lookup"><span data-stu-id="1bba6-259">Additional resources</span></span>

* [<span data-ttu-id="1bba6-260">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="1bba6-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1bba6-261">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1bba6-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

