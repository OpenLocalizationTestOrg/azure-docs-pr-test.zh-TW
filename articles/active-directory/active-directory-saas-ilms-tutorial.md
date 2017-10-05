---
title: "教學課程：Azure Active Directory 與 iLMS 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 iLMS 之間的單一登入。"
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
ms.openlocfilehash: 22c72020200138e78835ed7dd2661f18b824c785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="18070-103">教學課程：Azure Active Directory 與 iLMS 整合</span><span class="sxs-lookup"><span data-stu-id="18070-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="18070-104">在本教學課程中，您會了解如何將 iLMS 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="18070-104">In this tutorial, you learn how to integrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18070-105">iLMS 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="18070-105">Integrating iLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="18070-106">您可以在 Azure AD 中控制誰有 iLMS 的存取權</span><span class="sxs-lookup"><span data-stu-id="18070-106">You can control in Azure AD who has access to iLMS</span></span>
- <span data-ttu-id="18070-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 iLMS (單一登入)</span><span class="sxs-lookup"><span data-stu-id="18070-107">You can enable your users to automatically get signed-on to iLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18070-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="18070-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="18070-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="18070-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18070-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="18070-110">Prerequisites</span></span>

<span data-ttu-id="18070-111">若要設定 Azure AD 與 iLMS 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="18070-111">To configure Azure AD integration with iLMS, you need the following items:</span></span>

- <span data-ttu-id="18070-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="18070-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18070-113">啟用 iLMS 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="18070-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18070-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="18070-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18070-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="18070-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18070-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="18070-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="18070-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="18070-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18070-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="18070-118">Scenario description</span></span>
<span data-ttu-id="18070-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="18070-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18070-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="18070-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18070-121">從資源庫新增 iLMS</span><span class="sxs-lookup"><span data-stu-id="18070-121">Adding iLMS from the gallery</span></span>
2. <span data-ttu-id="18070-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="18070-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-the-gallery"></a><span data-ttu-id="18070-123">從資源庫新增 iLMS</span><span class="sxs-lookup"><span data-stu-id="18070-123">Adding iLMS from the gallery</span></span>
<span data-ttu-id="18070-124">若要設定將 iLMS 整合到 Azure AD 中，您需要從資源庫將 iLMS 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="18070-124">To configure the integration of iLMS into Azure AD, you need to add iLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="18070-125">**若要從資源庫新增 iLMS，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="18070-125">**To add iLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="18070-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="18070-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="18070-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="18070-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="18070-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="18070-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="18070-131">若要新增新的應用程式，按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="18070-131">To add new application, click **New application** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="18070-133">在搜尋方塊中，輸入 **iLMS**。</span><span class="sxs-lookup"><span data-stu-id="18070-133">In the search box, type **iLMS**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="18070-135">在結果窗格中，選取 [iLMS]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="18070-135">In the results panel, select **iLMS**, then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="18070-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="18070-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="18070-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 iLMS 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="18070-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="18070-139">若要讓單一登入運作，Azure AD 必須知道 iLMS 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="18070-139">For single sign-on to work, Azure AD needs to know what the counterpart user in iLMS is to a user in Azure AD.</span></span> <span data-ttu-id="18070-140">換句話說，必須在 Azure AD 使用者和 iLMS 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="18070-140">In other words, a link relationship between an Azure AD user and the related user in iLMS needs to be established.</span></span>

<span data-ttu-id="18070-141">建立此連結關聯性的方法，是將 Azure AD 中**使用者名稱**的值，指派為 iLMS 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="18070-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in iLMS.</span></span>

<span data-ttu-id="18070-142">若要設定及測試與 iLMS 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="18070-142">To configure and test Azure AD single sign-on with iLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="18070-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="18070-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="18070-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="18070-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18070-145">**[建立 iLMS 測試使用者](#creating-an-ilms-test-user)** - 使 iLMS 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="18070-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - to have a counterpart of Britta Simon in iLMS that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="18070-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="18070-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18070-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="18070-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="18070-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="18070-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="18070-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 iLMS 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="18070-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="18070-150">**若要設定與 iLMS 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="18070-150">**To configure Azure AD single sign-on with iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="18070-151">在 Azure 入口網站的 [iLMS] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="18070-151">In the Azure portal, on the **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="18070-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="18070-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="18070-155">如果您想要以 **IDP** 起始模式設定應用程式，請在 [iLMS 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="18070-155">On the **iLMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="18070-157">a.</span><span class="sxs-lookup"><span data-stu-id="18070-157">a.</span></span> <span data-ttu-id="18070-158">在 [識別碼] 文字方塊中，將您從 iLMS 系統管理入口網站中 SAML 設定的 [服務提供者] 區段複製的 [識別碼] 值貼上。</span><span class="sxs-lookup"><span data-stu-id="18070-158">In the **Identifier** textbox, paste the **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="18070-159">b.</span><span class="sxs-lookup"><span data-stu-id="18070-159">b.</span></span> <span data-ttu-id="18070-160">在 [回覆 URL] 文字方塊中，將您從 iLMS 系統管理入口網站中 SAML 設定的 [服務提供者] 區段複製的 [端點 (URL)] 值貼上，並包含下列模式：`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="18070-160">In the **Reply URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having the following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="18070-161">這個 '123456' 是識別項的範例值。</span><span class="sxs-lookup"><span data-stu-id="18070-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="18070-162">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]：</span><span class="sxs-lookup"><span data-stu-id="18070-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="18070-164">在 [登入 URL] 文字方塊中，將您從 iLMS 系統管理入口網站中 SAML 設定的 [服務提供者] 區段複製的 [端點 (URL)] 值貼上，如同：`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="18070-164">In the **Sign-on URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="18070-165">若要啟用 JIT 佈建，iLMS 應用程式會預期要有特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="18070-165">To enable JIT provisioning, iLMS application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="18070-166">設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="18070-166">Configure the following claims for this application.</span></span> <span data-ttu-id="18070-167">您可以在應用程式整合頁面的 [使用者屬性] 區段中，管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="18070-167">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="18070-168">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="18070-168">The following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="18070-170">建立 **Department, Region** 和 **Division** 屬性，並在 iLMS 中新增這些屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="18070-170">Create **Department, Region** and **Division** attributes and add the name of these attributes in iLMS.</span></span> <span data-ttu-id="18070-171">上述的所有屬性都是必要屬性。</span><span class="sxs-lookup"><span data-stu-id="18070-171">All these attributes shown above are required.</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="18070-172">您必須啟用 iLMS 中的 [建立無法辨識的使用者帳戶] 來對應這些屬性。</span><span class="sxs-lookup"><span data-stu-id="18070-172">You have to enable **Create Un-recognized User Account** in iLMS to map these attributes.</span></span> <span data-ttu-id="18070-173">請依照[這裡](http://support.inspiredelearning.com/customer/portal/articles/2204526)的指示，了解屬性的設定。</span><span class="sxs-lookup"><span data-stu-id="18070-173">Follow the instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) to get an idea on the attributes configuration.</span></span>

6. <span data-ttu-id="18070-174">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="18070-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="18070-175">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="18070-175">Attribute Name</span></span> | <span data-ttu-id="18070-176">屬性值</span><span class="sxs-lookup"><span data-stu-id="18070-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="18070-177">division</span><span class="sxs-lookup"><span data-stu-id="18070-177">division</span></span> | <span data-ttu-id="18070-178">user.department</span><span class="sxs-lookup"><span data-stu-id="18070-178">user.department</span></span> |
    | <span data-ttu-id="18070-179">region</span><span class="sxs-lookup"><span data-stu-id="18070-179">region</span></span> | <span data-ttu-id="18070-180">user.state</span><span class="sxs-lookup"><span data-stu-id="18070-180">user.state</span></span> |
    | <span data-ttu-id="18070-181">department</span><span class="sxs-lookup"><span data-stu-id="18070-181">department</span></span> | <span data-ttu-id="18070-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="18070-182">user.jobtitle</span></span> |

    <span data-ttu-id="18070-183">a.</span><span class="sxs-lookup"><span data-stu-id="18070-183">a.</span></span> <span data-ttu-id="18070-184">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="18070-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="18070-187">b.</span><span class="sxs-lookup"><span data-stu-id="18070-187">b.</span></span> <span data-ttu-id="18070-188">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="18070-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="18070-189">c.</span><span class="sxs-lookup"><span data-stu-id="18070-189">c.</span></span> <span data-ttu-id="18070-190">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="18070-190">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="18070-191">d.</span><span class="sxs-lookup"><span data-stu-id="18070-191">d.</span></span> <span data-ttu-id="18070-192">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="18070-192">Click **Ok**</span></span>

7. <span data-ttu-id="18070-193">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="18070-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="18070-195">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="18070-195">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="18070-197">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **iLMS 系統管理入口網站** 。</span><span class="sxs-lookup"><span data-stu-id="18070-197">In a different web browser window, log in to your **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="18070-198">按一下 [設定] 索引標籤下的 [SSO:SAML]，開啟 SAML 設定並執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="18070-198">Click **SSO:SAML** under **Settings** tab to open SAML settings and perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="18070-200">a.</span><span class="sxs-lookup"><span data-stu-id="18070-200">a.</span></span> <span data-ttu-id="18070-201">展開 [服務提供者] 區段，然後複製**識別碼**和**端點 (URL)** 值。</span><span class="sxs-lookup"><span data-stu-id="18070-201">Expand the **Service Provider** section and copy the **Identifier** and **Endpoint (URL)** value.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="18070-203">b.</span><span class="sxs-lookup"><span data-stu-id="18070-203">b.</span></span> <span data-ttu-id="18070-204">在 [識別提供者] 區段中，按一下 [匯入中繼資料]。</span><span class="sxs-lookup"><span data-stu-id="18070-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="18070-205">c.</span><span class="sxs-lookup"><span data-stu-id="18070-205">c.</span></span> <span data-ttu-id="18070-206">在 [SAML 簽章憑證] 區段中，選取從 Azure 入口網站下載的 [中繼資料] 檔案。</span><span class="sxs-lookup"><span data-stu-id="18070-206">Select the **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="18070-208">d.</span><span class="sxs-lookup"><span data-stu-id="18070-208">d.</span></span> <span data-ttu-id="18070-209">如果您想要啟用 JIT 佈建來建立無法辨識之使用者的 iLMS 帳戶，請遵循以下步驟︰</span><span class="sxs-lookup"><span data-stu-id="18070-209">If you want to enable JIT provisioning to create iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="18070-210">請勾選 [建立無法辨識的使用者帳戶]。</span><span class="sxs-lookup"><span data-stu-id="18070-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="18070-212">將 Azure AD 中的屬性與 iLMS 中的屬性進行對應。</span><span class="sxs-lookup"><span data-stu-id="18070-212">Map the attributes in Azure AD with the attributes in iLMS.</span></span> <span data-ttu-id="18070-213">在屬性資料行中，指定屬性名稱或預設值。</span><span class="sxs-lookup"><span data-stu-id="18070-213">In the attribute column, specify the attributes name or the default value.</span></span>

    <span data-ttu-id="18070-214">e.</span><span class="sxs-lookup"><span data-stu-id="18070-214">e.</span></span> <span data-ttu-id="18070-215">移至 [商務規則] 索引標籤，然後執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="18070-215">Go to **Business Rules** tab and perform the following steps:</span></span> 
        
       ![設定單一登入](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="18070-217">請勾選 [建立無法辨識的區域、事業處和部門]，來建立單一登入時尚未存在的區域、事業處和部門。</span><span class="sxs-lookup"><span data-stu-id="18070-217">Check **Create Un-recognized Regions, Divisions and Departments** to create Regions, Divisions, and Departments that do not already exist at the time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="18070-218">請勾選 [在登入期間更新使用者設定檔]，來指定使用者的設定檔是否隨著每個單一登入而更新。</span><span class="sxs-lookup"><span data-stu-id="18070-218">Check **Update User Profile During Sign-in** to specify whether the user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="18070-219">如果勾選 [更新使用者設定檔中非必要欄位的空白值] 選項，則登入時為空白的選擇性設定檔欄位也將會造成使用者的 iLMS 設定檔包含這些欄位的空白值。</span><span class="sxs-lookup"><span data-stu-id="18070-219">If the **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause the user’s iLMS profile to contain blank values for those fields.</span></span>
        
       - <span data-ttu-id="18070-220">請勾選 [傳送錯誤通知電子郵件]，並輸入您要接收錯誤通知電子郵件之使用者的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="18070-220">Check **Send Error Notification Email** and enter the email of the user where you want to receive the error notification email.</span></span>

11. <span data-ttu-id="18070-221">按一下 [儲存] 按鈕以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="18070-221">Click **Save** button to save the settings.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="18070-223">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="18070-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="18070-224">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="18070-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="18070-225">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18070-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="18070-226">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="18070-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="18070-227">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="18070-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="18070-229">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="18070-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="18070-230">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="18070-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18070-232">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="18070-232">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18070-234">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="18070-234">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18070-236">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="18070-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18070-238">a.</span><span class="sxs-lookup"><span data-stu-id="18070-238">a.</span></span> <span data-ttu-id="18070-239">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="18070-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18070-240">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="18070-240">b.</span></span> <span data-ttu-id="18070-241">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="18070-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18070-242">c.</span><span class="sxs-lookup"><span data-stu-id="18070-242">c.</span></span> <span data-ttu-id="18070-243">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="18070-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="18070-244">d.</span><span class="sxs-lookup"><span data-stu-id="18070-244">d.</span></span> <span data-ttu-id="18070-245">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="18070-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="18070-246">建立 iLMS 測試使用者</span><span class="sxs-lookup"><span data-stu-id="18070-246">Creating an iLMS test user</span></span>

<span data-ttu-id="18070-247">應用程式支援及時 (Just In Time) 使用者佈建，而在驗證之後，則會在應用程式中自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="18070-247">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="18070-248">如果在 iLMS 系統管理入口網站設定 SAML 組態期間，您已按下 [建立無法辨識的使用者帳戶] 核取方塊，JIT 就會正常運作。</span><span class="sxs-lookup"><span data-stu-id="18070-248">JIT will work, if you have clicked the **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="18070-249">如果您需要以手動方式建立使用者，請依照下列步驟進行︰</span><span class="sxs-lookup"><span data-stu-id="18070-249">If you need to create an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="18070-250">以系統管理員身分登入您的 iLMS 公司網站。</span><span class="sxs-lookup"><span data-stu-id="18070-250">Log in to your iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="18070-251">按一下[使用者] 索引標籤下的 [註冊使用者]開啟 [註冊使用者] 頁面。</span><span class="sxs-lookup"><span data-stu-id="18070-251">Click **“Register User”** under **Users** tab to open **Register User** page.</span></span> 
   
   ![新增員工](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="18070-253">在 [註冊使用者] 頁面上，執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="18070-253">On the **“Register User”** page, perform the following steps.</span></span>

    ![新增員工](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="18070-255">a.</span><span class="sxs-lookup"><span data-stu-id="18070-255">a.</span></span> <span data-ttu-id="18070-256">在 [名字] 文字方塊中輸入 Britta 這個名字。</span><span class="sxs-lookup"><span data-stu-id="18070-256">In the **First Name** textbox, type the first name Britta.</span></span>
   
    <span data-ttu-id="18070-257">b.</span><span class="sxs-lookup"><span data-stu-id="18070-257">b.</span></span> <span data-ttu-id="18070-258">在 [姓氏] 文字方塊中輸入 Simon 這個姓氏。</span><span class="sxs-lookup"><span data-stu-id="18070-258">In the **Last Name** textbox, type the last name Simon.</span></span>

    <span data-ttu-id="18070-259">c.</span><span class="sxs-lookup"><span data-stu-id="18070-259">c.</span></span> <span data-ttu-id="18070-260">在 [電子郵件識別碼] 文字方塊中，輸入 Britta Simon 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="18070-260">In the **Email ID** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="18070-261">d.</span><span class="sxs-lookup"><span data-stu-id="18070-261">d.</span></span> <span data-ttu-id="18070-262">在 [區域] 下拉式清單中，選取區域的值。</span><span class="sxs-lookup"><span data-stu-id="18070-262">In the **Region** dropdown, select the value for region.</span></span>

    <span data-ttu-id="18070-263">e.</span><span class="sxs-lookup"><span data-stu-id="18070-263">e.</span></span> <span data-ttu-id="18070-264">在 [事業處] 下拉式清單中，選取事業處的值。</span><span class="sxs-lookup"><span data-stu-id="18070-264">In the **Division** dropdown, select the value for division.</span></span>

    <span data-ttu-id="18070-265">f.</span><span class="sxs-lookup"><span data-stu-id="18070-265">f.</span></span> <span data-ttu-id="18070-266">在 [部門] 下拉式清單中，選取部門的值。</span><span class="sxs-lookup"><span data-stu-id="18070-266">In the **Department** dropdown, select the value for department.</span></span>

    <span data-ttu-id="18070-267">g.</span><span class="sxs-lookup"><span data-stu-id="18070-267">g.</span></span> <span data-ttu-id="18070-268">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="18070-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="18070-269">您也可以選取 [傳送註冊郵件] 核取方塊，將註冊郵件傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="18070-269">You can send registration mail to user by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="18070-270">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="18070-270">Assigning the Azure AD test user</span></span>

<span data-ttu-id="18070-271">在本節中，您會將 iLMS 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="18070-271">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to iLMS.</span></span>

![指派使用者][200] 

<span data-ttu-id="18070-273">**若要將 Britta Simon 指派給 iLMS，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="18070-273">**To assign Britta Simon to iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="18070-274">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="18070-274">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="18070-276">在應用程式清單中，選取 [iLMS]。</span><span class="sxs-lookup"><span data-stu-id="18070-276">In the applications list, select **iLMS**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="18070-278">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="18070-278">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="18070-280">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="18070-280">Click **Add** button.</span></span> <span data-ttu-id="18070-281">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="18070-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="18070-283">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="18070-283">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="18070-284">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="18070-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18070-285">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="18070-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="18070-286">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="18070-286">Testing single sign-on</span></span>

<span data-ttu-id="18070-287">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="18070-287">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="18070-288">當您在存取面板中按一下 [iLMS] 圖格時，系統應該會將您自動登入 iLMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="18070-288">When you click the iLMS tile in the Access Panel, you should get automatically signed-on to your iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18070-289">其他資源</span><span class="sxs-lookup"><span data-stu-id="18070-289">Additional resources</span></span>

* [<span data-ttu-id="18070-290">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="18070-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18070-291">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="18070-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

