---
title: "教學課程：Azure Active Directory 與 BetterWorks 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 BetterWorks 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 9803593124318ea82e5a8888cc5a95b5da84472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="3cc83-103">教學課程：Azure Active Directory 與 BetterWorks 整合</span><span class="sxs-lookup"><span data-stu-id="3cc83-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="3cc83-104">在此教學課程中，您學會如何 toointegrate BetterWorks 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="3cc83-104">In this tutorial, you learn how toointegrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3cc83-105">與 Azure AD 整合 BetterWorks 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="3cc83-105">Integrating BetterWorks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3cc83-106">您可以控制存取 tooBetterWorks Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="3cc83-106">You can control in Azure AD who has access tooBetterWorks</span></span>
- <span data-ttu-id="3cc83-107">您可以啟用您的使用者 tooautomatically get 登入 tooBetterWorks （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="3cc83-107">You can enable your users tooautomatically get signed-on tooBetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3cc83-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3cc83-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3cc83-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3cc83-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cc83-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3cc83-110">Prerequisites</span></span>

<span data-ttu-id="3cc83-111">tooconfigure BetterWorks 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="3cc83-111">tooconfigure Azure AD integration with BetterWorks, you need hello following items:</span></span>

- <span data-ttu-id="3cc83-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3cc83-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3cc83-113">已啟用 BetterWorks 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3cc83-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3cc83-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="3cc83-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3cc83-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3cc83-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3cc83-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3cc83-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3cc83-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="3cc83-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3cc83-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="3cc83-118">Scenario description</span></span>
<span data-ttu-id="3cc83-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3cc83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3cc83-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="3cc83-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3cc83-121">從 hello 圖庫加入 BetterWorks</span><span class="sxs-lookup"><span data-stu-id="3cc83-121">Adding BetterWorks from hello gallery</span></span>
2. <span data-ttu-id="3cc83-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3cc83-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-hello-gallery"></a><span data-ttu-id="3cc83-123">從 hello 圖庫加入 BetterWorks</span><span class="sxs-lookup"><span data-stu-id="3cc83-123">Adding BetterWorks from hello gallery</span></span>
<span data-ttu-id="3cc83-124">tooconfigure hello 整合 BetterWorks 到 Azure AD，您需要 tooadd BetterWorks hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3cc83-124">tooconfigure hello integration of BetterWorks into Azure AD, you need tooadd BetterWorks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3cc83-125">**tooadd BetterWorks 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3cc83-125">**tooadd BetterWorks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3cc83-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="3cc83-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3cc83-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3cc83-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3cc83-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3cc83-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="3cc83-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3cc83-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="3cc83-133">在 [hello] 搜尋方塊中，輸入**BetterWorks**。</span><span class="sxs-lookup"><span data-stu-id="3cc83-133">In hello search box, type **BetterWorks**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="3cc83-135">在 hello 結果 窗格中，選取  **BetterWorks**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3cc83-135">In hello results panel, select **BetterWorks**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3cc83-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3cc83-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3cc83-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 BetterWorks 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3cc83-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3cc83-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 BetterWorks 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="3cc83-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BetterWorks is tooa user in Azure AD.</span></span> <span data-ttu-id="3cc83-140">換句話說，Azure AD 使用者與 hello BetterWorks 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="3cc83-140">In other words, a link relationship between an Azure AD user and hello related user in BetterWorks needs toobe established.</span></span>

<span data-ttu-id="3cc83-141">BetterWorks 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3cc83-141">In BetterWorks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3cc83-142">tooconfigure 及 BetterWorks 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="3cc83-142">tooconfigure and test Azure AD single sign-on with BetterWorks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3cc83-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="3cc83-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3cc83-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="3cc83-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3cc83-145">**[建立測試使用者 BetterWorks](#creating-a-betterworks-test-user)**  -toohave 許 Simon BetterWorks 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="3cc83-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - toohave a counterpart of Britta Simon in BetterWorks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3cc83-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3cc83-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3cc83-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="3cc83-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3cc83-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3cc83-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3cc83-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 BetterWorks 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="3cc83-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="3cc83-150">**tooconfigure Azure AD 單一登入與 BetterWorks，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3cc83-150">**tooconfigure Azure AD single sign-on with BetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="3cc83-151">在 Azure 入口網站上 hello hello **BetterWorks**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="3cc83-151">In hello Azure portal, on hello **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="3cc83-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3cc83-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="3cc83-155">在 hello **BetterWorks 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP 初始化模式**:</span><span class="sxs-lookup"><span data-stu-id="3cc83-155">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="3cc83-157">a.</span><span class="sxs-lookup"><span data-stu-id="3cc83-157">a.</span></span> <span data-ttu-id="3cc83-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="3cc83-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="3cc83-159">b.</span><span class="sxs-lookup"><span data-stu-id="3cc83-159">b.</span></span> <span data-ttu-id="3cc83-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="3cc83-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="3cc83-161">在 hello **BetterWorks 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**SP 初始模式**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3cc83-161">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="3cc83-163">a.</span><span class="sxs-lookup"><span data-stu-id="3cc83-163">a.</span></span> <span data-ttu-id="3cc83-164">按一下 hello**顯示進階的 URL 設定**。</span><span class="sxs-lookup"><span data-stu-id="3cc83-164">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="3cc83-165">b.</span><span class="sxs-lookup"><span data-stu-id="3cc83-165">b.</span></span> <span data-ttu-id="3cc83-166">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="3cc83-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3cc83-167">這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="3cc83-167">These are not real values.</span></span> <span data-ttu-id="3cc83-168">更新這些值以 hello 回覆 URL 識別項和實際登入 URL。</span><span class="sxs-lookup"><span data-stu-id="3cc83-168">Update these values with hello Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="3cc83-169">請連絡[BetterWorks 支援小組](mailto:support@betterworks.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="3cc83-169">Contact [BetterWorks support team](mailto:support@betterworks.com) tooget these values.</span></span>
 
4. <span data-ttu-id="3cc83-170">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="3cc83-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="3cc83-172">BetterWorks 應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="3cc83-172">BetterWorks application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="3cc83-173">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="3cc83-173">Configure hello following claims for this application.</span></span> <span data-ttu-id="3cc83-174">您可以從 hello 管理 hello 這些屬性的值"**屬性**"hello 應用程式 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3cc83-174">You can manage hello values of these attributes from hello "**Attribute**" tab of hello application.</span></span> <span data-ttu-id="3cc83-175">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="3cc83-175">hello following screenshot shows an example for this.</span></span> 

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="3cc83-177">在 [hello **SAML 權杖屬性**] 對話方塊中，每個資料列 hello 下表中所示執行 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3cc83-177">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
   | <span data-ttu-id="3cc83-178">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="3cc83-178">Attribute Name</span></span> | <span data-ttu-id="3cc83-179">屬性值</span><span class="sxs-lookup"><span data-stu-id="3cc83-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="3cc83-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="3cc83-180">saml_token</span></span>     | <span data-ttu-id="3cc83-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="3cc83-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="3cc83-182">a.</span><span class="sxs-lookup"><span data-stu-id="3cc83-182">a.</span></span> <span data-ttu-id="3cc83-183">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3cc83-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="3cc83-186">b.</span><span class="sxs-lookup"><span data-stu-id="3cc83-186">b.</span></span> <span data-ttu-id="3cc83-187">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="3cc83-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

   <span data-ttu-id="3cc83-188">c.</span><span class="sxs-lookup"><span data-stu-id="3cc83-188">c.</span></span> <span data-ttu-id="3cc83-189">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="3cc83-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
   <span data-ttu-id="3cc83-190">d.</span><span class="sxs-lookup"><span data-stu-id="3cc83-190">d.</span></span> <span data-ttu-id="3cc83-191">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3cc83-191">Click **Ok**.</span></span>

7. <span data-ttu-id="3cc83-192">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3cc83-192">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3cc83-194">tooconfigure 單一登入上**BetterWorks**端，您需要下載 toosend hello**中繼資料 XML**太[BetterWorks 支援小組](mailto:support@betterworks.com)。</span><span class="sxs-lookup"><span data-stu-id="3cc83-194">tooconfigure single sign-on on **BetterWorks** side, you need toosend hello downloaded **Metadata XML** too[BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="3cc83-195">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="3cc83-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3cc83-196">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="3cc83-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3cc83-197">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3cc83-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3cc83-198">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3cc83-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="3cc83-199">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3cc83-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="3cc83-201">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3cc83-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3cc83-202">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="3cc83-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3cc83-204">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="3cc83-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3cc83-206">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="3cc83-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3cc83-208">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3cc83-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3cc83-210">a.</span><span class="sxs-lookup"><span data-stu-id="3cc83-210">a.</span></span> <span data-ttu-id="3cc83-211">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3cc83-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3cc83-212">b.</span><span class="sxs-lookup"><span data-stu-id="3cc83-212">b.</span></span> <span data-ttu-id="3cc83-213">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="3cc83-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3cc83-214">c.</span><span class="sxs-lookup"><span data-stu-id="3cc83-214">c.</span></span> <span data-ttu-id="3cc83-215">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="3cc83-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3cc83-216">d.</span><span class="sxs-lookup"><span data-stu-id="3cc83-216">d.</span></span> <span data-ttu-id="3cc83-217">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3cc83-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="3cc83-218">建立 BetterWorks 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3cc83-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="3cc83-219">在本節中，您會在 BetterWorks 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="3cc83-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="3cc83-220">使用[BetterWorks 支援小組](mailto:support@betterworks.com)tooadd hello hello BetterWorks 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="3cc83-220">Work with [BetterWorks support team](mailto:support@betterworks.com) tooadd hello users in hello BetterWorks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3cc83-221">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="3cc83-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3cc83-222">在本節中，您可以授與存取 tooBetterWorks 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3cc83-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBetterWorks.</span></span>

![指派使用者][200] 

<span data-ttu-id="3cc83-224">**tooassign 許 Simon tooBetterWorks，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3cc83-224">**tooassign Britta Simon tooBetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="3cc83-225">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3cc83-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3cc83-227">在 [hello] 應用程式清單中，選取**BetterWorks**。</span><span class="sxs-lookup"><span data-stu-id="3cc83-227">In hello applications list, select **BetterWorks**.</span></span>

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="3cc83-229">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="3cc83-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="3cc83-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3cc83-231">Click **Add** button.</span></span> <span data-ttu-id="3cc83-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3cc83-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="3cc83-234">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="3cc83-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3cc83-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3cc83-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3cc83-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3cc83-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3cc83-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3cc83-237">Testing single sign-on</span></span>

<span data-ttu-id="3cc83-238">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="3cc83-238">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3cc83-239">當您按一下的 hello BetterWorks 磚 hello 存取面板中時，您應該取得自動登入 tooyour BetterWorks 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3cc83-239">When you click hello BetterWorks tile in hello Access Panel, you should get automatically signed-on tooyour BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3cc83-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="3cc83-240">Additional resources</span></span>

* [<span data-ttu-id="3cc83-241">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3cc83-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3cc83-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3cc83-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

