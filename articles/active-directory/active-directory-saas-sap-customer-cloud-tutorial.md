---
title: "教學課程：Azure Active Directory 與 SAP Cloud for Customer 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與客戶的 SAP 雲端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="787ca-103">教學課程：Azure Active Directory 與 SAP Cloud for Customer 整合</span><span class="sxs-lookup"><span data-stu-id="787ca-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="787ca-104">在此教學課程中，您學習如何 toointegrate SAP 客戶與 Azure Active Directory (Azure AD) 的雲端。</span><span class="sxs-lookup"><span data-stu-id="787ca-104">In this tutorial, you learn how toointegrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="787ca-105">SAP 雲端整合與 Azure AD 的客戶可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="787ca-105">Integrating SAP Cloud for Customer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="787ca-106">您可以控制存取 tooSAP 雲端客戶的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="787ca-106">You can control in Azure AD who has access tooSAP Cloud for Customer</span></span>
- <span data-ttu-id="787ca-107">您可以啟用您的使用者 tooautomatically get 登入 tooSAP 雲端 （單一登入） 的客戶使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="787ca-107">You can enable your users tooautomatically get signed-on tooSAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="787ca-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="787ca-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="787ca-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="787ca-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="787ca-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="787ca-110">Prerequisites</span></span>

<span data-ttu-id="787ca-111">tooconfigure SAP 雲端與客戶的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="787ca-111">tooconfigure Azure AD integration with SAP Cloud for Customer, you need hello following items:</span></span>

- <span data-ttu-id="787ca-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="787ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="787ca-113">啟用 SAP Cloud for Customer 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="787ca-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="787ca-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="787ca-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="787ca-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="787ca-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="787ca-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="787ca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="787ca-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="787ca-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="787ca-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="787ca-118">Scenario description</span></span>
<span data-ttu-id="787ca-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="787ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="787ca-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="787ca-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="787ca-121">加入 SAP 雲端的客戶，從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="787ca-121">Adding SAP Cloud for Customer from hello gallery</span></span>
2. <span data-ttu-id="787ca-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="787ca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a><span data-ttu-id="787ca-123">加入 SAP 雲端的客戶，從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="787ca-123">Adding SAP Cloud for Customer from hello gallery</span></span>
<span data-ttu-id="787ca-124">tooconfigure hello 整合 SAP 雲端至 Azure AD 的客戶，您需要 tooadd SAP 雲端客戶的 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="787ca-124">tooconfigure hello integration of SAP Cloud for Customer into Azure AD, you need tooadd SAP Cloud for Customer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="787ca-125">**tooadd SAP 雲端客戶的 hello 圖庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="787ca-125">**tooadd SAP Cloud for Customer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="787ca-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="787ca-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="787ca-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="787ca-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="787ca-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="787ca-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="787ca-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="787ca-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="787ca-133">在 [hello] 搜尋方塊中，輸入**客戶的 SAP 雲端**。</span><span class="sxs-lookup"><span data-stu-id="787ca-133">In hello search box, type **SAP Cloud for Customer**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="787ca-135">在 [hello [結果] 窗格中，選取**SAP 雲端客戶的**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="787ca-135">In hello results panel, select **SAP Cloud for Customer**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="787ca-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="787ca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="787ca-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP Cloud for Customer 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="787ca-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="787ca-139">單一登入 toowork，Azure AD 需要 tooknow 客戶的 SAP 雲端中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="787ca-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Cloud for Customer is tooa user in Azure AD.</span></span> <span data-ttu-id="787ca-140">換句話說，Azure AD 使用者和客戶的 SAP 雲端中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="787ca-140">In other words, a link relationship between an Azure AD user and hello related user in SAP Cloud for Customer needs toobe established.</span></span>

<span data-ttu-id="787ca-141">在 SAP 雲端中的客戶，指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="787ca-141">In SAP Cloud for Customer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="787ca-142">tooconfigure 及測試 Azure AD 單一登入 SAP 雲端與客戶，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="787ca-142">tooconfigure and test Azure AD single sign-on with SAP Cloud for Customer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="787ca-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="787ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="787ca-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="787ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="787ca-145">**[建立 SAP 雲端客戶測試使用者](#creating-a-sap-cloud-for-customer-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示的客戶的 SAP 雲端中的對應項目。</span><span class="sxs-lookup"><span data-stu-id="787ca-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - toohave a counterpart of Britta Simon in SAP Cloud for Customer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="787ca-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="787ca-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="787ca-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="787ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="787ca-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="787ca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="787ca-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您的客戶應用程式的 SAP 雲端中。</span><span class="sxs-lookup"><span data-stu-id="787ca-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="787ca-150">**Azure AD 單一登入與 SAP 雲端客戶的 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="787ca-150">**tooconfigure Azure AD single sign-on with SAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="787ca-151">在 Azure 入口網站上 hello hello**客戶的 SAP 雲端**應用程式整合頁面上，按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="787ca-151">In hello Azure portal, on hello **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="787ca-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="787ca-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="787ca-155">在 [hello**客戶網域和 Url 的 SAP 雲端**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="787ca-155">On hello **SAP Cloud for Customer Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="787ca-157">a.</span><span class="sxs-lookup"><span data-stu-id="787ca-157">a.</span></span> <span data-ttu-id="787ca-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="787ca-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="787ca-159">b.</span><span class="sxs-lookup"><span data-stu-id="787ca-159">b.</span></span> <span data-ttu-id="787ca-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="787ca-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="787ca-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="787ca-161">These values are not real.</span></span> <span data-ttu-id="787ca-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="787ca-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="787ca-163">請連絡[客戶用戶端支援小組的 SAP 雲端](https://www.sap.com/about/agreements.sap-cloud-services-customers.html)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="787ca-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget these values.</span></span> 

4. <span data-ttu-id="787ca-164">在 [hello**使用者屬性**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="787ca-164">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="787ca-166">a.</span><span class="sxs-lookup"><span data-stu-id="787ca-166">a.</span></span> <span data-ttu-id="787ca-167">在**使用者識別碼**清單中，選取 hello **ExtractMailPrefix()**函式。</span><span class="sxs-lookup"><span data-stu-id="787ca-167">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="787ca-168">b.</span><span class="sxs-lookup"><span data-stu-id="787ca-168">b.</span></span> <span data-ttu-id="787ca-169">從 hello**郵件**清單中，您想要實作 toouse 選取 hello 使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="787ca-169">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="787ca-170">例如，如果您想 toouse hello EmployeeID 做為唯一的使用者識別碼，而且您已在 hello ExtensionAttribute2 儲存 hello 屬性值，然後選取 user.extensionattribute2。</span><span class="sxs-lookup"><span data-stu-id="787ca-170">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="787ca-171">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="787ca-171">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="787ca-173">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="787ca-173">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="787ca-175">在 hello**客戶設定的 SAP 雲端**區段中，按一下**客戶設定 SAP 雲端**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="787ca-175">On hello **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="787ca-176">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="787ca-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="787ca-178">tooget SSO 設定，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="787ca-178">tooget SSO configured, perform hello following steps:</span></span>
   
    <span data-ttu-id="787ca-179">a.</span><span class="sxs-lookup"><span data-stu-id="787ca-179">a.</span></span> <span data-ttu-id="787ca-180">使用系統管理員權限登入 SAP Cloud for Customer 入口網站。</span><span class="sxs-lookup"><span data-stu-id="787ca-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="787ca-181">b.</span><span class="sxs-lookup"><span data-stu-id="787ca-181">b.</span></span> <span data-ttu-id="787ca-182">瀏覽 toohello**應用程式和使用者管理的一般工作**按一下 hello**身分識別提供者**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="787ca-182">Navigate toohello **Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="787ca-183">c.</span><span class="sxs-lookup"><span data-stu-id="787ca-183">c.</span></span> <span data-ttu-id="787ca-184">按一下**新的身分識別提供者**和選取 hello 從 hello Azure 入口網站下載的中繼資料 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="787ca-184">Click **New Identity Provider** and select hello metadata XML file you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="787ca-185">匯入 hello 中繼資料，hello 系統會自動上傳 hello 需要的簽章憑證和加密憑證。</span><span class="sxs-lookup"><span data-stu-id="787ca-185">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="787ca-187">d.</span><span class="sxs-lookup"><span data-stu-id="787ca-187">d.</span></span> <span data-ttu-id="787ca-188">Azure Active Directory 需要 hello SAML 要求中的 hello 項目判斷提示取用者服務 URL 中，因此選取 hello**包括判斷提示取用者服務 URL**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="787ca-188">Azure Active Directory requires hello element Assertion Consumer Service URL in hello SAML request, so select hello **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="787ca-189">e.</span><span class="sxs-lookup"><span data-stu-id="787ca-189">e.</span></span> <span data-ttu-id="787ca-190">按一下 [啟用單一登入]。</span><span class="sxs-lookup"><span data-stu-id="787ca-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="787ca-191">f.</span><span class="sxs-lookup"><span data-stu-id="787ca-191">f.</span></span> <span data-ttu-id="787ca-192">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="787ca-192">Save your changes.</span></span>
   
    <span data-ttu-id="787ca-193">g.</span><span class="sxs-lookup"><span data-stu-id="787ca-193">g.</span></span> <span data-ttu-id="787ca-194">按一下 hello**我系統**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="787ca-194">Click hello **My System** tab.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="787ca-196">h.</span><span class="sxs-lookup"><span data-stu-id="787ca-196">h.</span></span> <span data-ttu-id="787ca-197">在 [Azure AD 登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 **SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="787ca-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="787ca-199">i.</span><span class="sxs-lookup"><span data-stu-id="787ca-199">i.</span></span> <span data-ttu-id="787ca-200">指定是否 hello 員工可以手動選擇選取 hello 登入以使用者識別碼和密碼或 SSO**手動身分識別提供者選取**。</span><span class="sxs-lookup"><span data-stu-id="787ca-200">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting hello **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="787ca-201">j.</span><span class="sxs-lookup"><span data-stu-id="787ca-201">j.</span></span> <span data-ttu-id="787ca-202">在 [hello **SSO URL**區段中，指定應由您的員工 toosign toohello 系統上的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="787ca-202">In hello **SSO URL** section, specify hello URL that should be used by your employees toosign on toohello system.</span></span> 
    <span data-ttu-id="787ca-203">在 [hello **URL 傳送 tooEmployee** ] 清單中，您可以選擇下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="787ca-203">In hello **URL Sent tooEmployee** list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="787ca-204">**非 SSO URL**</span><span class="sxs-lookup"><span data-stu-id="787ca-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="787ca-205">hello 系統會傳送只 hello 一般系統 URL toohello 員工。</span><span class="sxs-lookup"><span data-stu-id="787ca-205">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="787ca-206">hello 員工無法登入使用 SSO，且必須使用密碼或改為憑證。</span><span class="sxs-lookup"><span data-stu-id="787ca-206">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="787ca-207">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="787ca-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="787ca-208">hello 系統會傳送只 hello SSO URL toohello 員工。</span><span class="sxs-lookup"><span data-stu-id="787ca-208">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="787ca-209">hello 員工可以登入使用 SSO。</span><span class="sxs-lookup"><span data-stu-id="787ca-209">hello employee can log on using SSO.</span></span> <span data-ttu-id="787ca-210">驗證要求重新導向到 [hello IdP。</span><span class="sxs-lookup"><span data-stu-id="787ca-210">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="787ca-211">**自動選取**</span><span class="sxs-lookup"><span data-stu-id="787ca-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="787ca-212">如果並未啟用 SSO，hello 系統會傳送 hello 一般系統 URL toohello 員工。</span><span class="sxs-lookup"><span data-stu-id="787ca-212">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="787ca-213">如果 SSO 為作用中，hello 系統會檢查 hello 員工是否有密碼。</span><span class="sxs-lookup"><span data-stu-id="787ca-213">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="787ca-214">如果密碼功能，同時 SSO URL 和非 SSO URL 傳送 toohello 員工。</span><span class="sxs-lookup"><span data-stu-id="787ca-214">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="787ca-215">不過，如果 hello 員工沒有密碼，hello SSO URL 會傳送 toohello 員工。</span><span class="sxs-lookup"><span data-stu-id="787ca-215">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="787ca-216">k.</span><span class="sxs-lookup"><span data-stu-id="787ca-216">k.</span></span> <span data-ttu-id="787ca-217">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="787ca-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="787ca-218">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="787ca-218">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="787ca-219">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="787ca-219">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="787ca-220">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="787ca-220">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="787ca-221">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="787ca-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="787ca-222">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="787ca-222">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="787ca-224">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="787ca-224">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="787ca-225">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="787ca-225">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="787ca-227">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="787ca-227">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="787ca-229">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="787ca-229">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="787ca-231">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="787ca-231">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="787ca-233">a.</span><span class="sxs-lookup"><span data-stu-id="787ca-233">a.</span></span> <span data-ttu-id="787ca-234">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="787ca-234">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="787ca-235">b.</span><span class="sxs-lookup"><span data-stu-id="787ca-235">b.</span></span> <span data-ttu-id="787ca-236">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="787ca-236">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="787ca-237">c.</span><span class="sxs-lookup"><span data-stu-id="787ca-237">c.</span></span> <span data-ttu-id="787ca-238">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="787ca-238">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="787ca-239">d.</span><span class="sxs-lookup"><span data-stu-id="787ca-239">d.</span></span> <span data-ttu-id="787ca-240">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="787ca-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="787ca-241">建立 SAP Cloud for Customer 測試使用者</span><span class="sxs-lookup"><span data-stu-id="787ca-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="787ca-242">在本節中，您要在 SAP Cloud for Customer 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="787ca-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="787ca-243">請使用[客戶支援服務團隊的 SAP 雲端](https://www.sap.com/about/agreements.sap-cloud-services-customers.html)tooadd hello hello SAP 雲端客戶的平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="787ca-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd hello users in hello SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="787ca-244">請確定 NameID 值應該符合與 hello 客戶平台的 hello SAP 雲端中的使用者名稱欄位。</span><span class="sxs-lookup"><span data-stu-id="787ca-244">Please make sure that NameID value should match with hello username field in hello SAP Cloud for Customer platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="787ca-245">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="787ca-245">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="787ca-246">本節中，在您啟用 Azure 單一登入許 Simon toouse 客戶授與存取 tooSAP 雲端。</span><span class="sxs-lookup"><span data-stu-id="787ca-246">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Cloud for Customer.</span></span>

![指派使用者][200] 

<span data-ttu-id="787ca-248">**tooassign 許 Simon tooSAP 定域機組的客戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="787ca-248">**tooassign Britta Simon tooSAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="787ca-249">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="787ca-249">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="787ca-251">在 [hello] 應用程式清單中，選取**客戶的 SAP 雲端**。</span><span class="sxs-lookup"><span data-stu-id="787ca-251">In hello applications list, select **SAP Cloud for Customer**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="787ca-253">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="787ca-253">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="787ca-255">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="787ca-255">Click **Add** button.</span></span> <span data-ttu-id="787ca-256">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="787ca-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="787ca-258">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="787ca-258">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="787ca-259">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="787ca-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="787ca-260">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="787ca-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="787ca-261">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="787ca-261">Testing single sign-on</span></span>

<span data-ttu-id="787ca-262">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="787ca-262">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="787ca-263">當您按一下 hello SAP 雲端客戶磚 hello 存取面板中時，您應該取得自動登入 tooyour SAP 雲端客戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="787ca-263">When you click hello SAP Cloud for Customer tile in hello Access Panel, you should get automatically signed-on tooyour SAP Cloud for Customer application.</span></span>
<span data-ttu-id="787ca-264">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="787ca-264">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="787ca-265">其他資源</span><span class="sxs-lookup"><span data-stu-id="787ca-265">Additional resources</span></span>

* [<span data-ttu-id="787ca-266">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="787ca-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="787ca-267">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="787ca-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

