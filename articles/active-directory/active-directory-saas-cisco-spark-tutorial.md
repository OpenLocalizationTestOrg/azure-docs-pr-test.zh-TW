---
title: "教學課程：Azure Active Directory 與 Cisco Spark 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Cisco Spark 之間。"
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
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="ab13e-103">教學課程：Azure Active Directory 與 Cisco Spark 整合</span><span class="sxs-lookup"><span data-stu-id="ab13e-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="ab13e-104">在此教學課程中，您學會如何 toointegrate Cisco 二手與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ab13e-104">In this tutorial, you learn how toointegrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab13e-105">與 Azure AD 整合 Cisco Spark 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="ab13e-105">Integrating Cisco Spark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ab13e-106">您可以控制存取 tooCisco Spark Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="ab13e-106">You can control in Azure AD who has access tooCisco Spark</span></span>
- <span data-ttu-id="ab13e-107">您可以啟用您的使用者 tooautomatically get 登入 tooCisco Spark （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="ab13e-107">You can enable your users tooautomatically get signed-on tooCisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ab13e-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ab13e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ab13e-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ab13e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab13e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ab13e-110">Prerequisites</span></span>

<span data-ttu-id="ab13e-111">tooconfigure Azure AD 與 Cisco Spark 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="ab13e-111">tooconfigure Azure AD integration with Cisco Spark, you need hello following items:</span></span>

- <span data-ttu-id="ab13e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ab13e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab13e-113">已啟用 Cisco Spark 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ab13e-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ab13e-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="ab13e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ab13e-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ab13e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab13e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ab13e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ab13e-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ab13e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab13e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ab13e-118">Scenario description</span></span>
<span data-ttu-id="ab13e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ab13e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ab13e-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ab13e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab13e-121">從 hello 圖庫加入 Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="ab13e-121">Adding Cisco Spark from hello gallery</span></span>
2. <span data-ttu-id="ab13e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ab13e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-hello-gallery"></a><span data-ttu-id="ab13e-123">從 hello 圖庫加入 Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="ab13e-123">Adding Cisco Spark from hello gallery</span></span>
<span data-ttu-id="ab13e-124">tooconfigure hello 整合 Cisco Spark 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Cisco Spark。</span><span class="sxs-lookup"><span data-stu-id="ab13e-124">tooconfigure hello integration of Cisco Spark into Azure AD, you need tooadd Cisco Spark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ab13e-125">**tooadd Cisco Spark 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ab13e-125">**tooadd Cisco Spark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab13e-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ab13e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ab13e-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ab13e-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ab13e-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ab13e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ab13e-133">在 [hello] 搜尋方塊中，輸入**Cisco Spark**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-133">In hello search box, type **Cisco Spark**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="ab13e-135">在 hello 結果 窗格中，選取  **Cisco Spark**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab13e-135">In hello results panel, select **Cisco Spark**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ab13e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ab13e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ab13e-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Cisco Spark 設定和測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ab13e-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ab13e-139">單一登入 toowork，Azure AD 需要 tooknow Cisco Spark 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ab13e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cisco Spark is tooa user in Azure AD.</span></span> <span data-ttu-id="ab13e-140">換句話說，Azure AD 使用者與 Cisco Spark 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="ab13e-140">In other words, a link relationship between an Azure AD user and hello related user in Cisco Spark needs toobe established.</span></span>

<span data-ttu-id="ab13e-141">Cisco Spark 中指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ab13e-141">In Cisco Spark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ab13e-142">tooconfigure 及測試 Azure AD 單一登入與 Cisco Spark，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="ab13e-142">tooconfigure and test Azure AD single sign-on with Cisco Spark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ab13e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="ab13e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ab13e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="ab13e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab13e-145">**[建立測試使用者 Cisco Spark](#creating-a-cisco-spark-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Cisco Spark 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="ab13e-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - toohave a counterpart of Britta Simon in Cisco Spark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ab13e-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ab13e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab13e-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="ab13e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ab13e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ab13e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ab13e-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Cisco Spark 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="ab13e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="ab13e-150">**tooconfigure Azure AD 單一登入使用 Cisco Spark 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ab13e-150">**tooconfigure Azure AD single sign-on with Cisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab13e-151">在 Azure 入口網站上 hello hello **Cisco Spark**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-151">In hello Azure portal, on hello **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ab13e-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ab13e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="ab13e-155">在 hello **Cisco Spark 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab13e-155">On hello **Cisco Spark Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="ab13e-157">a.</span><span class="sxs-lookup"><span data-stu-id="ab13e-157">a.</span></span> <span data-ttu-id="ab13e-158">在 hello**登入 URL**文字方塊中，輸入與 URL:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="ab13e-158">In hello **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="ab13e-159">b.</span><span class="sxs-lookup"><span data-stu-id="ab13e-159">b.</span></span> <span data-ttu-id="ab13e-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="ab13e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ab13e-161">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="ab13e-161">This value is not real.</span></span> <span data-ttu-id="ab13e-162">更新此值以 hello 實際的識別項。</span><span class="sxs-lookup"><span data-stu-id="ab13e-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="ab13e-163">請連絡[Cisco Spark 用戶端支援小組](https://support.ciscospark.com/)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="ab13e-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) tooget this value.</span></span> 
 
4. <span data-ttu-id="ab13e-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="ab13e-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="ab13e-166">Cisco Spark 應用程式預期 hello SAML 判斷提示 toocontain 特定屬性。</span><span class="sxs-lookup"><span data-stu-id="ab13e-166">Cisco Spark application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="ab13e-167">設定下列屬性，此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="ab13e-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="ab13e-168">您可以從 hello 管理這些屬性的 hello 值**使用者屬性**應用程式整合頁面上的一節。</span><span class="sxs-lookup"><span data-stu-id="ab13e-168">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="ab13e-169">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="ab13e-169">hello following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="ab13e-171">在 hello**使用者屬性**區段 hello**單一登入** 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab13e-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="ab13e-172">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="ab13e-172">Attribute Name</span></span>  | <span data-ttu-id="ab13e-173">屬性值</span><span class="sxs-lookup"><span data-stu-id="ab13e-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="ab13e-174">UID</span><span class="sxs-lookup"><span data-stu-id="ab13e-174">uid</span></span>    | <span data-ttu-id="ab13e-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ab13e-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="ab13e-176">a.</span><span class="sxs-lookup"><span data-stu-id="ab13e-176">a.</span></span> <span data-ttu-id="ab13e-177">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ab13e-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ab13e-180">b.</span><span class="sxs-lookup"><span data-stu-id="ab13e-180">b.</span></span> <span data-ttu-id="ab13e-181">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="ab13e-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ab13e-182">c.</span><span class="sxs-lookup"><span data-stu-id="ab13e-182">c.</span></span> <span data-ttu-id="ab13e-183">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="ab13e-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ab13e-184">d.</span><span class="sxs-lookup"><span data-stu-id="ab13e-184">d.</span></span> <span data-ttu-id="ab13e-185">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ab13e-185">Click **Ok**.</span></span>

7. <span data-ttu-id="ab13e-186">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ab13e-186">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ab13e-188">登入太[Cisco 雲端共同作業管理](https://admin.ciscospark.com/)以完整系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="ab13e-188">Sign in too[Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="ab13e-189">選取**設定**在 hello**驗證**區段中，按一下**修改**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-189">Select **Settings** and under hello **Authentication** section, click **Modify**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="ab13e-191">選取 整合協力廠商識別提供者 **（進階）**和移 toohello 下一個畫面。</span><span class="sxs-lookup"><span data-stu-id="ab13e-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go toohello next screen.</span></span>

11. <span data-ttu-id="ab13e-192">在 hello**匯入 Idp 中繼資料**頁面上，可以拖曳和卸除 hello Azure AD 中繼資料檔案放入 hello 頁面或使用 hello 檔案瀏覽器選項 toolocate 並上傳 hello Azure AD 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="ab13e-192">On hello **Import Idp Metadata** page, either drag and drop hello Azure AD metadata file onto hello page or use hello file browser option toolocate and upload hello Azure AD metadata file.</span></span> <span data-ttu-id="ab13e-193">然後，選取 [需要中繼資料中憑證授權單位所簽署的憑證 (較安全)]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ab13e-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="ab13e-195">選取 [測試 SSO 連接]，並在新的瀏覽器索引標籤開啟時，透過登入向 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ab13e-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="ab13e-196">傳回 toohello **Cisco 雲端共同作業管理**瀏覽器索引標籤。如果 hello 測試成功，請選取**這項測試成功。**啟用單一登入 選項，然後按 下一步。</span><span class="sxs-lookup"><span data-stu-id="ab13e-196">Return toohello **Cisco Cloud Collaboration Management** browser tab. If hello test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="ab13e-197">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="ab13e-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ab13e-198">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="ab13e-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ab13e-199">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ab13e-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ab13e-200">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ab13e-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="ab13e-201">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ab13e-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ab13e-203">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ab13e-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab13e-204">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ab13e-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ab13e-206">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ab13e-208">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="ab13e-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ab13e-210">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab13e-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ab13e-212">a.</span><span class="sxs-lookup"><span data-stu-id="ab13e-212">a.</span></span> <span data-ttu-id="ab13e-213">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab13e-214">b.</span><span class="sxs-lookup"><span data-stu-id="ab13e-214">b.</span></span> <span data-ttu-id="ab13e-215">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="ab13e-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ab13e-216">c.</span><span class="sxs-lookup"><span data-stu-id="ab13e-216">c.</span></span> <span data-ttu-id="ab13e-217">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ab13e-218">d.</span><span class="sxs-lookup"><span data-stu-id="ab13e-218">d.</span></span> <span data-ttu-id="ab13e-219">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ab13e-219">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="ab13e-220">建立 Cisco Spark 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ab13e-220">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="ab13e-221">在本節中，您要在 Cisco Spark 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ab13e-221">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="ab13e-222">在本節中，您要在 Cisco Spark 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ab13e-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="ab13e-223">移 toohello [Cisco 雲端共同作業管理](https://admin.ciscospark.com/)以完整系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="ab13e-223">Go toohello [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="ab13e-224">按一下 [使用者]，然後按一下 [管理使用者]。</span><span class="sxs-lookup"><span data-stu-id="ab13e-224">Click **Users** and then **Manage Users**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="ab13e-226">在 [hello**管理使用者**視窗中，選取**手動新增或修改使用者**按一下**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-226">In hello **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="ab13e-227">選取 [名稱和電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="ab13e-227">Select **Names and Email address**.</span></span> <span data-ttu-id="ab13e-228">然後，填滿出 hello 文字方塊中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ab13e-228">Then, fill out hello textbox as follows:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="ab13e-230">a.</span><span class="sxs-lookup"><span data-stu-id="ab13e-230">a.</span></span> <span data-ttu-id="ab13e-231">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-231">In hello **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="ab13e-232">b.</span><span class="sxs-lookup"><span data-stu-id="ab13e-232">b.</span></span> <span data-ttu-id="ab13e-233">在 hello**姓氏**文字方塊中，輸入**Simon**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-233">In hello **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="ab13e-234">c.</span><span class="sxs-lookup"><span data-stu-id="ab13e-234">c.</span></span> <span data-ttu-id="ab13e-235">在 hello**電子郵件地址**文字方塊中，輸入 **britta.simon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="ab13e-235">In hello **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="ab13e-236">按一下 hello 加上簽章 tooadd 許 Simon。</span><span class="sxs-lookup"><span data-stu-id="ab13e-236">Click hello plus sign tooadd Britta Simon.</span></span> <span data-ttu-id="ab13e-237">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="ab13e-237">Then, click **Next**.</span></span>

6. <span data-ttu-id="ab13e-238">在 hello**新增使用者的服務**視窗中，按一下 **儲存**然後**完成**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-238">In hello **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ab13e-239">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="ab13e-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ab13e-240">在本節中，您可以授與存取 tooCisco Spark 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ab13e-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCisco Spark.</span></span>

![指派使用者][200] 

<span data-ttu-id="ab13e-242">**tooassign 許 Simon tooCisco Spark，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ab13e-242">**tooassign Britta Simon tooCisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab13e-243">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ab13e-245">在 [hello] 應用程式清單中，選取**Cisco Spark**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-245">In hello applications list, select **Cisco Spark**.</span></span>

    ![設定單一登入](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="ab13e-247">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="ab13e-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ab13e-249">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ab13e-249">Click **Add** button.</span></span> <span data-ttu-id="ab13e-250">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ab13e-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ab13e-252">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="ab13e-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ab13e-253">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ab13e-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab13e-254">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ab13e-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ab13e-255">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ab13e-255">Testing single sign-on</span></span>

<span data-ttu-id="ab13e-256">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="ab13e-256">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ab13e-257">當您按一下 hello Cisco Spark 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Cisco Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab13e-257">When you click hello Cisco Spark tile in hello Access Panel, you should get automatically signed-on tooyour Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ab13e-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="ab13e-258">Additional resources</span></span>

* [<span data-ttu-id="ab13e-259">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab13e-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab13e-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ab13e-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

