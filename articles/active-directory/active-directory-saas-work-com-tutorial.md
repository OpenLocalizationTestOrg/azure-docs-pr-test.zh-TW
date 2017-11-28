---
title: "教學課程：Azure Active Directory 與 Work.com 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Work.com 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="e459c-103">教學課程：Azure Active Directory 與 Work.com 整合</span><span class="sxs-lookup"><span data-stu-id="e459c-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="e459c-104">在此教學課程中，您學會如何 toointegrate Work.com 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e459c-104">In this tutorial, you learn how toointegrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e459c-105">與 Azure AD 整合 Work.com 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="e459c-105">Integrating Work.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e459c-106">您可以控制存取 tooWork.com Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="e459c-106">You can control in Azure AD who has access tooWork.com</span></span>
- <span data-ttu-id="e459c-107">您可以啟用您的使用者 tooautomatically get 登入 tooWork.com （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="e459c-107">You can enable your users tooautomatically get signed-on tooWork.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e459c-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e459c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e459c-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e459c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e459c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e459c-110">Prerequisites</span></span>

<span data-ttu-id="e459c-111">tooconfigure Azure AD 與 Work.com 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="e459c-111">tooconfigure Azure AD integration with Work.com, you need hello following items:</span></span>

- <span data-ttu-id="e459c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e459c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e459c-113">已啟用 Work.com 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e459c-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e459c-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="e459c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e459c-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e459c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e459c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e459c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e459c-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e459c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e459c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e459c-118">Scenario description</span></span>
<span data-ttu-id="e459c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e459c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e459c-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e459c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e459c-121">從 hello 圖庫新增 Work.com</span><span class="sxs-lookup"><span data-stu-id="e459c-121">Add Work.com from hello gallery</span></span>
2. <span data-ttu-id="e459c-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e459c-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-hello-gallery"></a><span data-ttu-id="e459c-123">從 hello 圖庫新增 Work.com</span><span class="sxs-lookup"><span data-stu-id="e459c-123">Add Work.com from hello gallery</span></span>
<span data-ttu-id="e459c-124">tooconfigure hello 整合 Work.com 到 Azure AD，您需要 tooadd Work.com hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e459c-124">tooconfigure hello integration of Work.com into Azure AD, you need tooadd Work.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e459c-125">**tooadd Work.com 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e459c-125">**tooadd Work.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e459c-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e459c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e459c-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e459c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e459c-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e459c-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e459c-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="e459c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e459c-133">在 [hello] 搜尋方塊中，輸入**Work.com**，選取**Work.com**從 [結果] 窗格按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e459c-133">In hello search box, type **Work.com**, select **Work.com** from results panel then click **Add** button tooadd hello application.</span></span>

    ![從資源庫新增](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e459c-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e459c-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="e459c-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Work.com 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e459c-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e459c-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Work.com 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="e459c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Work.com is tooa user in Azure AD.</span></span> <span data-ttu-id="e459c-138">換句話說，Azure AD 使用者與 hello Work.com 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="e459c-138">In other words, a link relationship between an Azure AD user and hello related user in Work.com needs toobe established.</span></span>

<span data-ttu-id="e459c-139">在 Work.com 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e459c-139">In Work.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e459c-140">tooconfigure 及 Azure AD 單一登入與 Work.com 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="e459c-140">tooconfigure and test Azure AD single sign-on with Work.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e459c-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="e459c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e459c-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="e459c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e459c-143">**[建立測試使用者 Work.com](#create-a-workcom-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Work.com 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="e459c-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - toohave a counterpart of Britta Simon in Work.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e459c-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e459c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e459c-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="e459c-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e459c-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e459c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e459c-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Work.com 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="e459c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="e459c-148">tooconfigure 單一登入，必須將自訂的 Work.com 網域名稱 toosetup 尚未。</span><span class="sxs-lookup"><span data-stu-id="e459c-148">tooconfigure single sign-on, you need toosetup a custom Work.com domain name yet.</span></span> <span data-ttu-id="e459c-149">您需要 toodefine 至少一個網域名稱、 測試您的網域名稱，並將它部署 tooyour 整個組織。</span><span class="sxs-lookup"><span data-stu-id="e459c-149">You need toodefine at least a domain name, test your domain name, and deploy it tooyour entire organization.</span></span>

<span data-ttu-id="e459c-150">**tooconfigure Azure AD 單一登入 Work.com 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e459c-150">**tooconfigure Azure AD single sign-on with Work.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="e459c-151">在 Azure 入口網站上 hello hello **Work.com**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="e459c-151">In hello Azure portal, on hello **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e459c-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e459c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="e459c-155">在 hello **Work.com 網域和 Url**區段中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="e459c-155">On hello **Work.com Domain and URLs** section, perform hello following:</span></span>

    ![[Work.com 網域與 URL] 區段](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="e459c-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="e459c-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e459c-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="e459c-158">This value is not real.</span></span> <span data-ttu-id="e459c-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="e459c-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e459c-160">請連絡[Work.com 用戶端支援小組](https://help.salesforce.com/articleView?id=000159855&type=3)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="e459c-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) tooget this value.</span></span> 

4. <span data-ttu-id="e459c-161">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="e459c-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="e459c-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e459c-163">Click **Save** button.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e459c-165">在 hello **Work.com 組態**區段中，按一下**設定 Work.com** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="e459c-165">On hello **Work.com Configuration** section, click **Configure Work.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e459c-166">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="e459c-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![[Work.com 設定] 區段](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="e459c-168">登入 tooyour Work.com 租用戶系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="e459c-168">Log in tooyour Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="e459c-169">跳過**安裝**。</span><span class="sxs-lookup"><span data-stu-id="e459c-169">Go too**Setup**.</span></span>
   
    <span data-ttu-id="e459c-170">![設定](./media/active-directory-saas-work-com-tutorial/ic794108.png "設定")</span><span class="sxs-lookup"><span data-stu-id="e459c-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="e459c-171">在 hello 左側瀏覽窗格中，在 hello**管理**區段中，按一下**定義域管理**tooexpand hello 相關的區段，然後按一下**我的網域**tooopen hello **我的網域**頁面。</span><span class="sxs-lookup"><span data-stu-id="e459c-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
    <span data-ttu-id="e459c-172">![我的網域](./media/active-directory-saas-work-com-tutorial/ic767825.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="e459c-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="e459c-173">tooverify，您的網域是否已正確設定，請確定它是在 「**步驟 4 部署 tooUsers**」，並檢閱您"**我的網域設定**"。</span><span class="sxs-lookup"><span data-stu-id="e459c-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="e459c-174">![網域部署 tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "網域部署 tooUser")</span><span class="sxs-lookup"><span data-stu-id="e459c-174">![Domain Deployed tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="e459c-175">登入 tooyour Work.com 租用戶。</span><span class="sxs-lookup"><span data-stu-id="e459c-175">Log in tooyour Work.com tenant.</span></span>

12. <span data-ttu-id="e459c-176">跳過**安裝**。</span><span class="sxs-lookup"><span data-stu-id="e459c-176">Go too**Setup**.</span></span>
    
    <span data-ttu-id="e459c-177">![設定](./media/active-directory-saas-work-com-tutorial/ic794108.png "設定")</span><span class="sxs-lookup"><span data-stu-id="e459c-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="e459c-178">展開 hello**安全性控制**功能表，然後再按一下**單一登入設定**。</span><span class="sxs-lookup"><span data-stu-id="e459c-178">Expand hello **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="e459c-179">![單一登入設定](./media/active-directory-saas-work-com-tutorial/ic794113.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="e459c-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="e459c-180">在 hello**單一登入設定**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e459c-180">On hello **Single Sign-On Settings** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="e459c-181">![啟用 SAML](./media/active-directory-saas-work-com-tutorial/ic781026.png "啟用 SAML")</span><span class="sxs-lookup"><span data-stu-id="e459c-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="e459c-182">a.</span><span class="sxs-lookup"><span data-stu-id="e459c-182">a.</span></span> <span data-ttu-id="e459c-183">選取 [已啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="e459c-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="e459c-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e459c-184">b.</span></span> <span data-ttu-id="e459c-185">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="e459c-185">Click **New**.</span></span>

15. <span data-ttu-id="e459c-186">在 hello **SAML 單一登入設定**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e459c-186">In hello **SAML Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="e459c-187">![SAML 單一登入設定](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML 單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="e459c-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="e459c-188">a.</span><span class="sxs-lookup"><span data-stu-id="e459c-188">a.</span></span> <span data-ttu-id="e459c-189">在 hello**名稱**文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="e459c-189">In hello **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="e459c-190">提供值**名稱**自動填入 hello **API 名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e459c-190">Providing a value for **Name** does automatically populate hello **API Name** textbox.</span></span>
    
    <span data-ttu-id="e459c-191">b.</span><span class="sxs-lookup"><span data-stu-id="e459c-191">b.</span></span> <span data-ttu-id="e459c-192">在**簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="e459c-192">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="e459c-193">c.</span><span class="sxs-lookup"><span data-stu-id="e459c-193">c.</span></span> <span data-ttu-id="e459c-194">從 Azure 入口網站的 tooupload hello 下載憑證，請按一下**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="e459c-194">tooupload hello downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="e459c-195">d.</span><span class="sxs-lookup"><span data-stu-id="e459c-195">d.</span></span> <span data-ttu-id="e459c-196">在 hello**實體識別碼**文字方塊中，輸入`https://salesforce-work.com`。</span><span class="sxs-lookup"><span data-stu-id="e459c-196">In hello **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="e459c-197">e.</span><span class="sxs-lookup"><span data-stu-id="e459c-197">e.</span></span> <span data-ttu-id="e459c-198">做為**SAML 識別類型**，選取**判斷提示包含從 hello 使用者物件的同盟識別碼 hello**。</span><span class="sxs-lookup"><span data-stu-id="e459c-198">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
    
    <span data-ttu-id="e459c-199">f.</span><span class="sxs-lookup"><span data-stu-id="e459c-199">f.</span></span> <span data-ttu-id="e459c-200">做為**SAML 識別位置**，選取**身分識別位於 Subject 陳述式 hello hello NameIdentfier 元素**。</span><span class="sxs-lookup"><span data-stu-id="e459c-200">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>
    
    <span data-ttu-id="e459c-201">g.</span><span class="sxs-lookup"><span data-stu-id="e459c-201">g.</span></span> <span data-ttu-id="e459c-202">在**身分識別提供者登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="e459c-202">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e459c-203">h.</span><span class="sxs-lookup"><span data-stu-id="e459c-203">h.</span></span> <span data-ttu-id="e459c-204">在**身分識別提供者登出 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="e459c-204">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="e459c-205">i.</span><span class="sxs-lookup"><span data-stu-id="e459c-205">i.</span></span> <span data-ttu-id="e459c-206">在 [服務提供者起始的要求繫結]，選取 [HTTP Post]。</span><span class="sxs-lookup"><span data-stu-id="e459c-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="e459c-207">j.</span><span class="sxs-lookup"><span data-stu-id="e459c-207">j.</span></span> <span data-ttu-id="e459c-208">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e459c-208">Click **Save**.</span></span>

16. <span data-ttu-id="e459c-209">在您的 Work.com 傳統入口網站在 hello 左側瀏覽窗格中，按一下**定義域管理**tooexpand hello 相關的區段，然後按一下**我的網域**tooopen hello**我的網域**頁面。</span><span class="sxs-lookup"><span data-stu-id="e459c-209">In your Work.com classic portal, on hello left navigation pane, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="e459c-210">![我的網域](./media/active-directory-saas-work-com-tutorial/ic794115.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="e459c-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="e459c-211">在 [hello**我的網域**] 頁面的 hello**登入頁面品牌**區段中，按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="e459c-211">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="e459c-212">![登入頁面商標](./media/active-directory-saas-work-com-tutorial/ic767826.png "登入頁面商標")</span><span class="sxs-lookup"><span data-stu-id="e459c-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="e459c-213">在 hello**登入頁面品牌** 頁面的 hello**驗證服務**區段、 hello 名稱您**SAML SSO 設定**隨即出現。</span><span class="sxs-lookup"><span data-stu-id="e459c-213">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="e459c-214">請選取該名稱，然後按一下儲存 。</span><span class="sxs-lookup"><span data-stu-id="e459c-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="e459c-215">![登入頁面商標](./media/active-directory-saas-work-com-tutorial/ic784366.png "登入頁面商標")</span><span class="sxs-lookup"><span data-stu-id="e459c-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="e459c-216">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="e459c-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e459c-217">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="e459c-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e459c-218">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e459c-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e459c-219">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e459c-219">Create an Azure AD test user</span></span>
<span data-ttu-id="e459c-220">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e459c-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e459c-222">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e459c-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e459c-223">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e459c-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e459c-225">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="e459c-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] -> [所有使用者]](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e459c-227">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="e459c-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![加](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e459c-229">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e459c-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![使用者對話方塊頁面](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e459c-231">a.</span><span class="sxs-lookup"><span data-stu-id="e459c-231">a.</span></span> <span data-ttu-id="e459c-232">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e459c-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e459c-233">b.</span><span class="sxs-lookup"><span data-stu-id="e459c-233">b.</span></span> <span data-ttu-id="e459c-234">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="e459c-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e459c-235">c.</span><span class="sxs-lookup"><span data-stu-id="e459c-235">c.</span></span> <span data-ttu-id="e459c-236">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="e459c-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e459c-237">d.</span><span class="sxs-lookup"><span data-stu-id="e459c-237">d.</span></span> <span data-ttu-id="e459c-238">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e459c-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="e459c-239">建立 Work.com 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e459c-239">Create a Work.com test user</span></span>
<span data-ttu-id="e459c-240">Azure Active Directory 使用者 toobe 無法 toosign 中，它們必須已佈建的 tooWork.com。在 Work.com 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="e459c-240">For Azure Active Directory users toobe able toosign in, they must be provisioned tooWork.com. In hello case of Work.com, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="e459c-241">tooconfigure 使用者佈建，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e459c-241">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="e459c-242">登入 tooyour Work.com 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="e459c-242">Sign on tooyour Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="e459c-243">跳過**安裝**。</span><span class="sxs-lookup"><span data-stu-id="e459c-243">Go too**Setup**.</span></span>
   
    <span data-ttu-id="e459c-244">![設定](./media/active-directory-saas-work-com-tutorial/IC794108.png "設定")</span><span class="sxs-lookup"><span data-stu-id="e459c-244">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="e459c-245">跳過**管理使用者\>使用者**。</span><span class="sxs-lookup"><span data-stu-id="e459c-245">Go too**Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="e459c-246">![管理使用者](./media/active-directory-saas-work-com-tutorial/IC784369.png "管理使用者")</span><span class="sxs-lookup"><span data-stu-id="e459c-246">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="e459c-247">按一下 [新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="e459c-247">Click **New User**.</span></span>
   
    <span data-ttu-id="e459c-248">![所有使用者](./media/active-directory-saas-work-com-tutorial/IC794117.png "所有使用者")</span><span class="sxs-lookup"><span data-stu-id="e459c-248">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="e459c-249">在 hello 編輯使用者 區段中，執行下列步驟，在屬性的有效 azure 的 hello 想成 hello tooprovision AD 帳戶相關的文字方塊：</span><span class="sxs-lookup"><span data-stu-id="e459c-249">In hello User Edit section, perform hello following steps, in attributes of a valid Azure AD account you want tooprovision into hello related textboxes:</span></span>
   
    <span data-ttu-id="e459c-250">![使用者編輯](./media/active-directory-saas-work-com-tutorial/ic794118.png "使用者編輯")</span><span class="sxs-lookup"><span data-stu-id="e459c-250">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="e459c-251">a.</span><span class="sxs-lookup"><span data-stu-id="e459c-251">a.</span></span> <span data-ttu-id="e459c-252">在 hello**名字**文字方塊中，型別 hello**名字**hello 使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="e459c-252">In hello **First Name** textbox, type hello **first name** of hello user **Britta**.</span></span>
    
    <span data-ttu-id="e459c-253">b.</span><span class="sxs-lookup"><span data-stu-id="e459c-253">b.</span></span> <span data-ttu-id="e459c-254">在 hello**姓氏**文字方塊中，型別 hello**姓氏**hello 使用者的**Simon**。</span><span class="sxs-lookup"><span data-stu-id="e459c-254">In hello **Last Name** textbox, type hello **last name** of hello user **Simon**.</span></span>
    
    <span data-ttu-id="e459c-255">c.</span><span class="sxs-lookup"><span data-stu-id="e459c-255">c.</span></span> <span data-ttu-id="e459c-256">在 hello**別名**文字方塊中，型別 hello**名稱**hello 使用者的**BrittaS**。</span><span class="sxs-lookup"><span data-stu-id="e459c-256">In hello **Alias** textbox, type hello **name** of hello user **BrittaS**.</span></span>
    
    <span data-ttu-id="e459c-257">d.</span><span class="sxs-lookup"><span data-stu-id="e459c-257">d.</span></span> <span data-ttu-id="e459c-258">在 hello**電子郵件**文字方塊中，型別 hello**電子郵件地址**使用者的 **Brittasimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="e459c-258">In hello **Email** textbox, type hello **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="e459c-259">e.</span><span class="sxs-lookup"><span data-stu-id="e459c-259">e.</span></span> <span data-ttu-id="e459c-260">在 hello**使用者名**使用者的使用者名稱文字方塊中，輸入要 **Brittasimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="e459c-260">In hello **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="e459c-261">f.</span><span class="sxs-lookup"><span data-stu-id="e459c-261">f.</span></span> <span data-ttu-id="e459c-262">在 hello**別名**文字方塊中，輸入**別名**使用者的**Simon**。</span><span class="sxs-lookup"><span data-stu-id="e459c-262">In hello **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="e459c-263">g.</span><span class="sxs-lookup"><span data-stu-id="e459c-263">g.</span></span> <span data-ttu-id="e459c-264">選取 [角色]、[使用者授權] 和 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="e459c-264">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="e459c-265">h.</span><span class="sxs-lookup"><span data-stu-id="e459c-265">h.</span></span> <span data-ttu-id="e459c-266">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e459c-266">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="e459c-267">hello Azure AD 帳戶持有者會收到包含連結 tooconfirm hello 帳戶之前它會變成作用中的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e459c-267">hello Azure AD account holder will get an email including a link tooconfirm hello account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e459c-268">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e459c-268">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e459c-269">在本節中，您可以授與存取 tooWork.com 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e459c-269">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWork.com.</span></span>

![指派使用者][200] 

<span data-ttu-id="e459c-271">**tooassign 許 Simon tooWork.com，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e459c-271">**tooassign Britta Simon tooWork.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="e459c-272">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e459c-272">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e459c-274">在 [hello] 應用程式清單中，選取**Work.com**。</span><span class="sxs-lookup"><span data-stu-id="e459c-274">In hello applications list, select **Work.com**.</span></span>

    ![應用程式清單中的 Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="e459c-276">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="e459c-276">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e459c-278">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e459c-278">Click **Add** button.</span></span> <span data-ttu-id="e459c-279">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e459c-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e459c-281">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="e459c-281">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e459c-282">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e459c-282">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e459c-283">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e459c-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e459c-284">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e459c-284">Test single sign-on</span></span>

<span data-ttu-id="e459c-285">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="e459c-285">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e459c-286">當您按一下 hello Work.com 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Work.com 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e459c-286">When you click hello Work.com tile in hello Access Panel, you should get automatically signed-on tooyour Work.com application.</span></span>
<span data-ttu-id="e459c-287">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e459c-287">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e459c-288">其他資源</span><span class="sxs-lookup"><span data-stu-id="e459c-288">Additional resources</span></span>

* [<span data-ttu-id="e459c-289">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e459c-289">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e459c-290">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e459c-290">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

