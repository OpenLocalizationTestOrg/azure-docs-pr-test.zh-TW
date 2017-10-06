---
title: "教學課程：Azure Active Directory 與 Salesforce 沙箱整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Salesforce 沙箱之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="b6a10-103">教學課程：Azure Active Directory 與 Salesforce 沙箱整合</span><span class="sxs-lookup"><span data-stu-id="b6a10-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="b6a10-104">在此教學課程中，您學會如何 toointegrate 與 Azure Active Directory (Azure AD) 的 Salesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="b6a10-104">In this tutorial, you learn how toointegrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b6a10-105">整合 Azure AD 與 Salesforce 沙箱可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="b6a10-105">Integrating Salesforce Sandbox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b6a10-106">您可以控制存取 tooSalesforce 沙箱的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="b6a10-106">You can control in Azure AD who has access tooSalesforce Sandbox</span></span>
- <span data-ttu-id="b6a10-107">您可以啟用您的使用者 tooautomatically get 登入 tooSalesforce （單一登入） 的沙箱與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="b6a10-107">You can enable your users tooautomatically get signed-on tooSalesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b6a10-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b6a10-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b6a10-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b6a10-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6a10-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b6a10-110">Prerequisites</span></span>

<span data-ttu-id="b6a10-111">tooconfigure Azure AD 與 Salesforce 沙箱的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b6a10-111">tooconfigure Azure AD integration with Salesforce Sandbox, you need hello following items:</span></span>

- <span data-ttu-id="b6a10-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b6a10-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b6a10-113">啟用 Salesforce Sandbox 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b6a10-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b6a10-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b6a10-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b6a10-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b6a10-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b6a10-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b6a10-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b6a10-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b6a10-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b6a10-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b6a10-118">Scenario description</span></span>
<span data-ttu-id="b6a10-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b6a10-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b6a10-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b6a10-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b6a10-121">從 hello 圖庫加入 Salesforce 沙箱</span><span class="sxs-lookup"><span data-stu-id="b6a10-121">Adding Salesforce Sandbox from hello gallery</span></span>
2. <span data-ttu-id="b6a10-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b6a10-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a><span data-ttu-id="b6a10-123">從 hello 圖庫加入 Salesforce 沙箱</span><span class="sxs-lookup"><span data-stu-id="b6a10-123">Adding Salesforce Sandbox from hello gallery</span></span>
<span data-ttu-id="b6a10-124">tooconfigure hello 整合 Salesforce 沙箱到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Salesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="b6a10-124">tooconfigure hello integration of Salesforce Sandbox into Azure AD, you need tooadd Salesforce Sandbox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b6a10-125">**tooadd Salesforce 沙箱 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b6a10-125">**tooadd Salesforce Sandbox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6a10-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b6a10-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b6a10-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b6a10-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b6a10-131">按一下**新的應用程式**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b6a10-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b6a10-133">在 [hello] 搜尋方塊中，輸入**Salesforce 沙箱**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-133">In hello search box, type **Salesforce Sandbox**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="b6a10-135">在 [hello [結果] 窗格中，選取 [ **Salesforce 沙箱**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b6a10-135">In hello results panel, select **Salesforce Sandbox**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b6a10-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b6a10-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b6a10-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Salesforce Sandbox 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b6a10-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b6a10-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 [Salesforce 沙箱是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b6a10-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce Sandbox is tooa user in Azure AD.</span></span> <span data-ttu-id="b6a10-140">換句話說，Azure AD 使用者與 Salesforce 沙箱中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="b6a10-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce Sandbox needs toobe established.</span></span>

<span data-ttu-id="b6a10-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Salesforce 沙箱中。</span><span class="sxs-lookup"><span data-stu-id="b6a10-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="b6a10-142">tooconfigure 和測試 Azure AD 單一登入與 Salesforce 沙箱，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b6a10-142">tooconfigure and test Azure AD single sign-on with Salesforce Sandbox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b6a10-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b6a10-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b6a10-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="b6a10-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b6a10-145">**[建立 Salesforce 沙箱測試使用者](#creating-a-salesforce-sandbox-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Salesforce 沙箱中對應項目。</span><span class="sxs-lookup"><span data-stu-id="b6a10-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - toohave a counterpart of Britta Simon in Salesforce Sandbox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b6a10-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b6a10-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b6a10-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="b6a10-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b6a10-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b6a10-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b6a10-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Salesforce 沙箱應用程式中。</span><span class="sxs-lookup"><span data-stu-id="b6a10-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="b6a10-150">**tooconfigure Azure AD 單一登入與 Salesforce 沙箱，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b6a10-150">**tooconfigure Azure AD single sign-on with Salesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6a10-151">在 Azure 入口網站上 hello hello **Salesforce 沙箱**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-151">In hello Azure portal, on hello **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b6a10-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b6a10-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="b6a10-155">在 [hello **Salesforce 沙箱網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6a10-155">On hello **Salesforce Sandbox Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="b6a10-157">在 [hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="b6a10-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b6a10-158">這個值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="b6a10-158">This value is not hello real.</span></span> <span data-ttu-id="b6a10-159">更新此值與 hello 實際登入 URL。請連絡[Salesforce 沙箱用戶端支援小組](https://help.salesforce.com/support)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="b6a10-159">Update this value with hello actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) tooget this value.</span></span>


4. <span data-ttu-id="b6a10-160">如果您已經在您目錄中，設定單一登入另一個 Salesforce 沙箱的執行個體，則您也必須設定 hello**識別碼**toohave hello 相同的值為 hello**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="b6a10-161">hello**識別碼**欄位可以找到藉由檢查 hello**顯示進階設定**hello 上的核取方塊**設定應用程式 URL** hello 對話方塊頁面</span><span class="sxs-lookup"><span data-stu-id="b6a10-161">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog</span></span> 


5. <span data-ttu-id="b6a10-162">在 [hello **SAML 簽章憑證**區段中，按一下**憑證**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="b6a10-162">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="b6a10-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b6a10-164">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b6a10-166">在 [hello **Salesforce 沙箱設定**區段中，按一下**設定 Salesforce 沙箱**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="b6a10-166">On hello **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b6a10-167">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="b6a10-167">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="b6a10-168">![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="b6a10-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="b6a10-169">在您的瀏覽器中開啟新索引標籤，並登入 tooyour Salesforce 沙箱管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6a10-169">Open a new tab in your browser and log in tooyour Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="b6a10-170">在 [hello 最上層顯示 hello 功能表上，按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-170">In hello menu on hello top, click **Setup**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="b6a10-172">Hello hello 左側瀏覽窗格中按一下**安全性控制**，然後按一下 [**單一登入設定**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-172">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="b6a10-174">Hello 單一登入設定] 區段中，執行下列步驟的 hello:![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="b6a10-174">On hello Single Sign-On Settings section, perform hello following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="b6a10-175">a.</span><span class="sxs-lookup"><span data-stu-id="b6a10-175">a.</span></span>  <span data-ttu-id="b6a10-176">選取 [已啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="b6a10-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="b6a10-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b6a10-177">b.</span></span>  <span data-ttu-id="b6a10-178">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="b6a10-178">Click **New**.</span></span>

12. <span data-ttu-id="b6a10-179">在 hello SAML 單一登入設定] 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6a10-179">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="b6a10-181">a.In hello 名稱文字方塊中，型別 hello hello 組態名稱 (例如： *SPSSOWAAD\_測試*)。</span><span class="sxs-lookup"><span data-stu-id="b6a10-181">a.In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="b6a10-182">b.</span><span class="sxs-lookup"><span data-stu-id="b6a10-182">b.</span></span> <span data-ttu-id="b6a10-183">貼上**SMAL 實體識別碼**值傳入 hello**簽發者**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b6a10-183">Paste **SMAL Entity ID** value into hello **Issuer** textbox.</span></span>

    <span data-ttu-id="b6a10-184">c.</span><span class="sxs-lookup"><span data-stu-id="b6a10-184">c.</span></span> <span data-ttu-id="b6a10-185">在 [hello**實體識別碼**文字方塊中，輸入**https://test.salesforce.com**便 hello 第一個您要加入 tooyour 目錄的 Salesforce 沙箱執行個體。</span><span class="sxs-lookup"><span data-stu-id="b6a10-185">In hello **Entity Id** textbox, type **https://test.salesforce.com** if it is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="b6a10-186">如果您已新增執行個體的 Salesforce 沙箱則 hello**實體識別碼**hello 中的型別**登入 URL**，應該採用下列格式：`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="b6a10-186">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="b6a10-187">d.</span><span class="sxs-lookup"><span data-stu-id="b6a10-187">d.</span></span> <span data-ttu-id="b6a10-188">按一下**瀏覽**tooupload hello 下載憑證。</span><span class="sxs-lookup"><span data-stu-id="b6a10-188">Click **Browse** tooupload hello downloaded certificate.</span></span>  

    <span data-ttu-id="b6a10-189">e.</span><span class="sxs-lookup"><span data-stu-id="b6a10-189">e.</span></span> <span data-ttu-id="b6a10-190">做為**SAML 識別類型**，選取**判斷提示包含從 hello 使用者物件的同盟識別碼 hello**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-190">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
 
    <span data-ttu-id="b6a10-191">f.</span><span class="sxs-lookup"><span data-stu-id="b6a10-191">f.</span></span> <span data-ttu-id="b6a10-192">做為**SAML 識別位置**，選取**hello 的 hello Subject 陳述式的 NameIdentifier 元素中的識別是**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-192">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="b6a10-193">g.</span><span class="sxs-lookup"><span data-stu-id="b6a10-193">g.</span></span> <span data-ttu-id="b6a10-194">貼上**單一登入服務 URL**到 hello**身分識別提供者登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b6a10-194">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="b6a10-195">h.</span><span class="sxs-lookup"><span data-stu-id="b6a10-195">h.</span></span> <span data-ttu-id="b6a10-196">SFDC 不支援 SAML 登出。</span><span class="sxs-lookup"><span data-stu-id="b6a10-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="b6a10-197">因應措施是，貼上 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' hello 到**身分識別提供者登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b6a10-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="b6a10-198">i.</span><span class="sxs-lookup"><span data-stu-id="b6a10-198">i.</span></span> <span data-ttu-id="b6a10-199">在 [服務提供者起始的要求繫結]，選取 [HTTP POST]。</span><span class="sxs-lookup"><span data-stu-id="b6a10-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="b6a10-200">j.</span><span class="sxs-lookup"><span data-stu-id="b6a10-200">j.</span></span> <span data-ttu-id="b6a10-201">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b6a10-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="b6a10-202">啟用網域</span><span class="sxs-lookup"><span data-stu-id="b6a10-202">Enable your domain</span></span>
<span data-ttu-id="b6a10-203">本節假設您已經建立了一個網域。</span><span class="sxs-lookup"><span data-stu-id="b6a10-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="b6a10-204">如需詳細資訊，請參閱[定義您的網域名稱](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)。</span><span class="sxs-lookup"><span data-stu-id="b6a10-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="b6a10-205">**tooenable 您的網域，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b6a10-205">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6a10-206">在 [hello 左側瀏覽窗格中，按一下 [**定義域管理**，然後按一下 [**我的網域。**</span><span class="sxs-lookup"><span data-stu-id="b6a10-206">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="b6a10-208">請確定您的網域已正確設定。</span><span class="sxs-lookup"><span data-stu-id="b6a10-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="b6a10-209">在 hello**登入頁面設定**區段中，按一下**編輯**，然後當**驗證服務**，選取 hello 名稱從先前的 hello hello SAML 單一登入設定區段，然後按一下 [最後**儲存**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-209">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="b6a10-211">當您設定網域之後，您的使用者應該使用 hello 網域 URL toologin toohello Salesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="b6a10-211">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="b6a10-212">hello URL 的 tooget hello 值，按一下您已建立 hello 前一節中的 hello SSO 設定檔。</span><span class="sxs-lookup"><span data-stu-id="b6a10-212">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="b6a10-213">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="b6a10-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b6a10-214">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="b6a10-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b6a10-215">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b6a10-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b6a10-216">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b6a10-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="b6a10-217">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b6a10-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b6a10-219">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b6a10-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6a10-220">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b6a10-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b6a10-222">使用者 toodisplay hello 清單太移**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-222">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b6a10-224">在 [hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b6a10-224">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b6a10-226">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6a10-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b6a10-228">a.</span><span class="sxs-lookup"><span data-stu-id="b6a10-228">a.</span></span> <span data-ttu-id="b6a10-229">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b6a10-230">b.</span><span class="sxs-lookup"><span data-stu-id="b6a10-230">b.</span></span> <span data-ttu-id="b6a10-231">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="b6a10-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b6a10-232">c.</span><span class="sxs-lookup"><span data-stu-id="b6a10-232">c.</span></span> <span data-ttu-id="b6a10-233">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b6a10-234">d.</span><span class="sxs-lookup"><span data-stu-id="b6a10-234">d.</span></span> <span data-ttu-id="b6a10-235">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b6a10-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="b6a10-236">建立 Salesforce Sandbox 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b6a10-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="b6a10-237">本節會在 Salesforce Sandbox 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="b6a10-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="b6a10-238">Salesforce Sandbox 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="b6a10-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="b6a10-239">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="b6a10-239">There is no action item for you in this section.</span></span> <span data-ttu-id="b6a10-240">如果使用者不存在於 Salesforce 沙箱，當您嘗試 tooaccess Salesforce 沙箱時，會建立一個新。</span><span class="sxs-lookup"><span data-stu-id="b6a10-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt tooaccess Salesforce Sandbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b6a10-241">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="b6a10-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b6a10-242">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooSalesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="b6a10-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce Sandbox.</span></span>

![指派使用者][200] 

<span data-ttu-id="b6a10-244">**tooassign 許 Simon tooSalesforce 沙箱，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b6a10-244">**tooassign Britta Simon tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6a10-245">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b6a10-247">在 [hello] 應用程式清單中，選取**Salesforce 沙箱**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-247">In hello applications list, select **Salesforce Sandbox**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="b6a10-249">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="b6a10-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b6a10-251">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b6a10-251">Click **Add** button.</span></span> <span data-ttu-id="b6a10-252">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b6a10-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b6a10-254">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="b6a10-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b6a10-255">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b6a10-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b6a10-256">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b6a10-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b6a10-257">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b6a10-257">Testing single sign-on</span></span>

<span data-ttu-id="b6a10-258">如果您想 tootest SSO 設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="b6a10-258">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="b6a10-259">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b6a10-259">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b6a10-260">其他資源</span><span class="sxs-lookup"><span data-stu-id="b6a10-260">Additional resources</span></span>

* [<span data-ttu-id="b6a10-261">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6a10-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b6a10-262">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b6a10-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b6a10-263">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="b6a10-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

