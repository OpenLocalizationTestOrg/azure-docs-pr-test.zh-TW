---
title: "教學課程：Azure Active Directory 與 IQNavigator VMS 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 IQNavigator VM 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="f1592-103">教學課程：Azure Active Directory 與 IQNavigator VMS 整合</span><span class="sxs-lookup"><span data-stu-id="f1592-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="f1592-104">在此教學課程中，您學會如何 toointegrate IQNavigator VM 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="f1592-104">In this tutorial, you learn how toointegrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1592-105">與 Azure AD 整合 IQNavigator VM 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="f1592-105">Integrating IQNavigator VMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1592-106">您可以控制存取 tooIQNavigator VM 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="f1592-106">You can control in Azure AD who has access tooIQNavigator VMS</span></span>
- <span data-ttu-id="f1592-107">您可以啟用您的使用者 tooautomatically get 登入 tooIQNavigator （單一登入） 的 VM 與 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="f1592-107">You can enable your users tooautomatically get signed-on tooIQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1592-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f1592-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f1592-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f1592-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1592-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f1592-110">Prerequisites</span></span>

<span data-ttu-id="f1592-111">tooconfigure IQNavigator VM 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="f1592-111">tooconfigure Azure AD integration with IQNavigator VMS, you need hello following items:</span></span>

- <span data-ttu-id="f1592-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f1592-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1592-113">啟用 IQNavigator VMS 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f1592-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1592-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="f1592-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1592-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f1592-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1592-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f1592-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1592-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="f1592-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1592-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f1592-118">Scenario description</span></span>
<span data-ttu-id="f1592-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1592-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1592-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="f1592-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1592-121">從 hello 圖庫加入 IQNavigator VM</span><span class="sxs-lookup"><span data-stu-id="f1592-121">Adding IQNavigator VMS from hello gallery</span></span>
2. <span data-ttu-id="f1592-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f1592-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a><span data-ttu-id="f1592-123">從 hello 圖庫加入 IQNavigator VM</span><span class="sxs-lookup"><span data-stu-id="f1592-123">Adding IQNavigator VMS from hello gallery</span></span>
<span data-ttu-id="f1592-124">tooconfigure hello 整合 IQNavigator VM 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd IQNavigator VM。</span><span class="sxs-lookup"><span data-stu-id="f1592-124">tooconfigure hello integration of IQNavigator VMS into Azure AD, you need tooadd IQNavigator VMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1592-125">**tooadd IQNavigator VM 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f1592-125">**tooadd IQNavigator VMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1592-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="f1592-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1592-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f1592-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f1592-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f1592-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f1592-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1592-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f1592-133">在 [hello] 搜尋方塊中，輸入**IQNavigator VM**。</span><span class="sxs-lookup"><span data-stu-id="f1592-133">In hello search box, type **IQNavigator VMS**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="f1592-135">在 hello 結果 窗格中，選取  **IQNavigator VM**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1592-135">In hello results panel, select **IQNavigator VMS**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1592-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f1592-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1592-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 IQNavigator VMS 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1592-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1592-139">單一登入 toowork，Azure AD 需要 tooknow IQNavigator VM 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="f1592-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IQNavigator VMS is tooa user in Azure AD.</span></span> <span data-ttu-id="f1592-140">換句話說，Azure AD 使用者與 hello IQNavigator VM 中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="f1592-140">In other words, a link relationship between an Azure AD user and hello related user in IQNavigator VMS needs toobe established.</span></span>

<span data-ttu-id="f1592-141">IQNavigator VM 中指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f1592-141">In IQNavigator VMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f1592-142">tooconfigure 及 IQNavigator VM 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="f1592-142">tooconfigure and test Azure AD single sign-on with IQNavigator VMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1592-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="f1592-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1592-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="f1592-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1592-145">**[建立測試使用者 IQNavigator VM](#creating-a-iqnavigator-vms-test-user)**  -toohave 許 Simon IQNavigator VM 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="f1592-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - toohave a counterpart of Britta Simon in IQNavigator VMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1592-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1592-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1592-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="f1592-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1592-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f1592-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1592-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 IQNavigator VM 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1592-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="f1592-150">**tooconfigure Azure AD 單一登入與 IQNavigator VM 執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f1592-150">**tooconfigure Azure AD single sign-on with IQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1592-151">在 Azure 入口網站上 hello hello **IQNavigator VM**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="f1592-151">In hello Azure portal, on hello **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f1592-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1592-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="f1592-155">在 hello **IQNavigator VM 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1592-155">On hello **IQNavigator VMS Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="f1592-157">a.</span><span class="sxs-lookup"><span data-stu-id="f1592-157">a.</span></span> <span data-ttu-id="f1592-158">在 hello**識別碼**文字方塊中，型別 hello URL:`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="f1592-158">In hello **Identifier** textbox, type hello URL:`iqn.com`</span></span>

    <span data-ttu-id="f1592-159">b.</span><span class="sxs-lookup"><span data-stu-id="f1592-159">b.</span></span> <span data-ttu-id="f1592-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="f1592-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="f1592-161">請檢查**顯示進階的 URL 設定**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1592-161">Check **Show advanced URL settings**, perform hello following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="f1592-163">在 hello**轉送狀態**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="f1592-163">In hello **Relay state** textbox, type a URL using hello following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1592-164">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="f1592-164">These values are not real.</span></span> <span data-ttu-id="f1592-165">更新這些值與 hello 實際的回覆 URL 和轉送狀態。</span><span class="sxs-lookup"><span data-stu-id="f1592-165">Update these values with hello actual Reply URL and Relay state.</span></span> <span data-ttu-id="f1592-166">請連絡[IQNavigator VM 用戶端支援小組](https://www.beeline.com/iqn-product-support/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="f1592-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) tooget these values.</span></span> 

5. <span data-ttu-id="f1592-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1592-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f1592-169">toogenerate hello**中繼資料**url，請執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1592-169">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="f1592-170">a.</span><span class="sxs-lookup"><span data-stu-id="f1592-170">a.</span></span> <span data-ttu-id="f1592-171">按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="f1592-171">Click **App registrations**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="f1592-173">b.</span><span class="sxs-lookup"><span data-stu-id="f1592-173">b.</span></span> <span data-ttu-id="f1592-174">按一下**端點**tooopen**端點** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f1592-174">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="f1592-176">c.</span><span class="sxs-lookup"><span data-stu-id="f1592-176">c.</span></span> <span data-ttu-id="f1592-177">按一下 hello 複製按鈕 toocopy**同盟中繼資料文件**url 並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="f1592-177">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="f1592-179">d.</span><span class="sxs-lookup"><span data-stu-id="f1592-179">d.</span></span> <span data-ttu-id="f1592-180">現在請 toohello 屬性頁的**IQNavigator VM**和複製 hello**應用程式識別碼**使用**複製**按鈕，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="f1592-180">Now go toohello property page of **IQNavigator VMS** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="f1592-182">e.</span><span class="sxs-lookup"><span data-stu-id="f1592-182">e.</span></span> <span data-ttu-id="f1592-183">產生 hello**中繼資料 URL**使用 hello 下列模式：`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="f1592-183">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="f1592-184">IQNavigator 應用程式預期 hello 名稱識別碼宣告中的 hello 唯一的使用者識別碼值。</span><span class="sxs-lookup"><span data-stu-id="f1592-184">IQNavigator application expect hello unique user identifier value in hello Name Identifier claim.</span></span> <span data-ttu-id="f1592-185">客戶可以將對應 hello 正確 hello 名稱識別碼宣告值。</span><span class="sxs-lookup"><span data-stu-id="f1592-185">Customer can map hello correct value for hello Name Identifier claim.</span></span> <span data-ttu-id="f1592-186">在此情況下，我們有對應 hello 使用者。UserPrincipalName hello 示範用途。</span><span class="sxs-lookup"><span data-stu-id="f1592-186">In this case we have mapped hello user.UserPrincipalName for hello demo purpose.</span></span> <span data-ttu-id="f1592-187">但是，根據 tooyour 組織設定您應該對應 hello 正確的值為它。</span><span class="sxs-lookup"><span data-stu-id="f1592-187">But according tooyour organization settings you should map hello correct value for it.</span></span>   

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="f1592-189">在 hello **IQNavigator VM 組態**區段中，按一下**設定 IQNavigator VM** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="f1592-189">On hello **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f1592-190">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="f1592-190">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="f1592-192">tooconfigure 單一登入上**IQNavigator VM**側邊，您需要 toosend hello**中繼資料 URL**，**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**太[IQNavigator VM 支援小組](https://www.beeline.com/iqn-product-support/)。</span><span class="sxs-lookup"><span data-stu-id="f1592-192">tooconfigure single sign-on on **IQNavigator VMS** side, you need toosend hello **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="f1592-193">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="f1592-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f1592-194">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="f1592-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f1592-195">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="f1592-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f1592-196">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1592-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1592-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f1592-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1592-198">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f1592-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f1592-200">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f1592-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1592-201">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="f1592-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1592-203">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="f1592-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1592-205">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="f1592-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1592-207">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1592-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1592-209">a.</span><span class="sxs-lookup"><span data-stu-id="f1592-209">a.</span></span> <span data-ttu-id="f1592-210">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f1592-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1592-211">b.</span><span class="sxs-lookup"><span data-stu-id="f1592-211">b.</span></span> <span data-ttu-id="f1592-212">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="f1592-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1592-213">c.</span><span class="sxs-lookup"><span data-stu-id="f1592-213">c.</span></span> <span data-ttu-id="f1592-214">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="f1592-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f1592-215">d.</span><span class="sxs-lookup"><span data-stu-id="f1592-215">d.</span></span> <span data-ttu-id="f1592-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f1592-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="f1592-217">建立 IQNavigator VM 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f1592-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="f1592-218">hello 本節目標在於 toocreate 呼叫許 Simon IQNavigator VM 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="f1592-218">hello objective of this section is toocreate a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="f1592-219">使用[IQNavigator VM 支援小組](https://www.beeline.com/iqn-product-support/)tooadd hello hello IQNavigator VM 帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="f1592-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) tooadd hello users in hello IQNavigator VMS account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f1592-220">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="f1592-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f1592-221">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooIQNavigator VM。</span><span class="sxs-lookup"><span data-stu-id="f1592-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIQNavigator VMS.</span></span>

![指派使用者][200] 

<span data-ttu-id="f1592-223">**tooassign 許 Simon tooIQNavigator VM，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f1592-223">**tooassign Britta Simon tooIQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1592-224">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f1592-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f1592-226">在 [hello] 應用程式清單中，選取**IQNavigator VM**。</span><span class="sxs-lookup"><span data-stu-id="f1592-226">In hello applications list, select **IQNavigator VMS**.</span></span>

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="f1592-228">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="f1592-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f1592-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1592-230">Click **Add** button.</span></span> <span data-ttu-id="f1592-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f1592-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f1592-233">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="f1592-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f1592-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1592-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1592-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1592-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1592-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f1592-236">Testing single sign-on</span></span>

<span data-ttu-id="f1592-237">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="f1592-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f1592-238">當您按一下 hello IQNavigator VM 磚 hello 存取面板中時，您應該取得自動登入 tooyour IQNavigator VM 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1592-238">When you click hello IQNavigator VMS tile in hello Access Panel, you should get automatically signed-on tooyour IQNavigator VMS application.</span></span>
<span data-ttu-id="f1592-239">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="f1592-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1592-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="f1592-240">Additional resources</span></span>

* [<span data-ttu-id="f1592-241">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1592-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1592-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f1592-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

