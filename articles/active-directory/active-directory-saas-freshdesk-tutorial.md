---
title: "教學課程：Azure Active Directory 與 FreshDesk 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 FreshDesk 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="82a26-103">教學課程：Azure Active Directory 與 FreshDesk 整合</span><span class="sxs-lookup"><span data-stu-id="82a26-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="82a26-104">在此教學課程中，您學會如何 toointegrate FreshDesk 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="82a26-104">In this tutorial, you learn how toointegrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82a26-105">整合 Azure AD 與 FreshDesk 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="82a26-105">Integrating FreshDesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="82a26-106">您可以控制存取 tooFreshDesk Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="82a26-106">You can control in Azure AD who has access tooFreshDesk</span></span>
- <span data-ttu-id="82a26-107">您可以啟用您的使用者 tooautomatically get 登入 tooFreshDesk （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="82a26-107">You can enable your users tooautomatically get signed-on tooFreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="82a26-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="82a26-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="82a26-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="82a26-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82a26-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="82a26-110">Prerequisites</span></span>

<span data-ttu-id="82a26-111">tooconfigure Azure AD 與 FreshDesk 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="82a26-111">tooconfigure Azure AD integration with FreshDesk, you need hello following items:</span></span>

- <span data-ttu-id="82a26-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="82a26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82a26-113">啟用 FreshDesk 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="82a26-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82a26-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="82a26-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82a26-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="82a26-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82a26-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="82a26-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="82a26-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="82a26-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82a26-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="82a26-118">Scenario description</span></span>
<span data-ttu-id="82a26-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="82a26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82a26-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="82a26-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82a26-121">從 hello 圖庫加入 FreshDesk</span><span class="sxs-lookup"><span data-stu-id="82a26-121">Adding FreshDesk from hello gallery</span></span>
2. <span data-ttu-id="82a26-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="82a26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-hello-gallery"></a><span data-ttu-id="82a26-123">從 hello 圖庫加入 FreshDesk</span><span class="sxs-lookup"><span data-stu-id="82a26-123">Adding FreshDesk from hello gallery</span></span>
<span data-ttu-id="82a26-124">tooconfigure hello 整合 FreshDesk 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd FreshDesk。</span><span class="sxs-lookup"><span data-stu-id="82a26-124">tooconfigure hello integration of FreshDesk into Azure AD, you need tooadd FreshDesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="82a26-125">**tooadd FreshDesk 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="82a26-125">**tooadd FreshDesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a26-126">在 [hello ** [Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="82a26-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="82a26-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="82a26-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="82a26-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="82a26-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="82a26-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="82a26-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="82a26-133">在 [hello] 搜尋方塊中，輸入**FreshDesk**。</span><span class="sxs-lookup"><span data-stu-id="82a26-133">In hello search box, type **FreshDesk**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="82a26-135">在 [hello [結果] 窗格中，選取 [ **FreshDesk**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="82a26-135">In hello results panel, select **FreshDesk**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="82a26-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="82a26-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="82a26-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FreshDesk 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="82a26-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="82a26-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 FreshDesk 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="82a26-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshDesk is tooa user in Azure AD.</span></span> <span data-ttu-id="82a26-140">換句話說，Azure AD 使用者與 hello FreshDesk 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="82a26-140">In other words, a link relationship between an Azure AD user and hello related user in FreshDesk needs toobe established.</span></span>

<span data-ttu-id="82a26-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** FreshDesk 中。</span><span class="sxs-lookup"><span data-stu-id="82a26-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FreshDesk.</span></span>

<span data-ttu-id="82a26-142">tooconfigure 和測試 Azure AD 單一登入與 FreshDesk，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="82a26-142">tooconfigure and test Azure AD single sign-on with FreshDesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="82a26-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="82a26-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="82a26-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="82a26-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="82a26-145">**[建立測試使用者 FreshDesk](#creating-a-freshdesk-test-user) ** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 FreshDesk 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="82a26-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - toohave a counterpart of Britta Simon in FreshDesk that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="82a26-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="82a26-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="82a26-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="82a26-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="82a26-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="82a26-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="82a26-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並設定單一登入 Freshservice 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="82a26-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="82a26-150">**tooconfigure Azure AD 單一登入 FreshDesk 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="82a26-150">**tooconfigure Azure AD single sign-on with FreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a26-151">在 hello Azure 管理入口網站上 hello **FreshDesk**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="82a26-151">In hello Azure Management portal, on hello **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="82a26-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="82a26-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="82a26-155">在 [hello **FreshDesk 網域和 Url**區段中，請輸入 hello**登入 URL**做為：`https://<tenant-name>.freshdesk.com`或 Freshdesk 有建議的任何其他值。</span><span class="sxs-lookup"><span data-stu-id="82a26-155">On hello **FreshDesk Domain and URLs** section, please enter hello **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="82a26-157">請注意，這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="82a26-157">Please note that this is not the real value.</span></span> <span data-ttu-id="82a26-158">您必須使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="82a26-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="82a26-159">請連絡 [FreshDesk 用戶端支援小組](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="82a26-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="82a26-160">在 [hello **SAML 簽章憑證**區段中，按一下**憑證**，然後儲存您的電腦上的 [hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="82a26-160">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="82a26-162">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="82a26-162">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="82a26-164">在 [hello **FreshDesk 組態**區段中，按一下**設定 FreshDesk** tooopen 設定登入視窗。</span><span class="sxs-lookup"><span data-stu-id="82a26-164">On hello **FreshDesk Configuration** section, click **Configure FreshDesk** tooopen Configure sign-on window.</span></span> <span data-ttu-id="82a26-165">Hello SAML 單一登入服務 URL 和登出 URL 複製 hello**快速參考**> 一節。</span><span class="sxs-lookup"><span data-stu-id="82a26-165">Copy hello SAML Single Sign-On Service URL and Sign-Out URL from hello **Quick Reference** section.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="82a26-167">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Freshdesk 公司網站。</span><span class="sxs-lookup"><span data-stu-id="82a26-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="82a26-168">在 [hello 最上層顯示 hello 功能表上，按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="82a26-168">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="82a26-169">![管理](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "管理")</span><span class="sxs-lookup"><span data-stu-id="82a26-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="82a26-170">在 [hello**一般設定**索引標籤上，按一下 [**安全性**。</span><span class="sxs-lookup"><span data-stu-id="82a26-170">In hello **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="82a26-171">![安全性](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="82a26-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="82a26-172">在 [hello**安全性**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="82a26-172">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="82a26-173">![單一登入](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="82a26-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="82a26-174">a.</span><span class="sxs-lookup"><span data-stu-id="82a26-174">a.</span></span> <span data-ttu-id="82a26-175">針對 [單一登入 (SSO)] 選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="82a26-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="82a26-176">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="82a26-176">b.</span></span> <span data-ttu-id="82a26-177">選取 [SAML SSO] 。</span><span class="sxs-lookup"><span data-stu-id="82a26-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="82a26-178">c.</span><span class="sxs-lookup"><span data-stu-id="82a26-178">c.</span></span> <span data-ttu-id="82a26-179">型別 hello **SAML 單一登入服務 URL**您從 Azure 入口網站複製到 hello **SAML 登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="82a26-179">Type hello **SAML Single Sign-On Service URL** you copied from Azure portal into hello **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="82a26-180">d.</span><span class="sxs-lookup"><span data-stu-id="82a26-180">d.</span></span> <span data-ttu-id="82a26-181">型別 hello**登出 URL**您從 Azure 入口網站複製到 hello**登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="82a26-181">Type hello **Sign-Out URL**  you copied from Azure portal into hello **Logout URL** textbox.</span></span>

    <span data-ttu-id="82a26-182">e.</span><span class="sxs-lookup"><span data-stu-id="82a26-182">e.</span></span> <span data-ttu-id="82a26-183">複製 hello**指紋**真品從 Azure 入口網站下載的 hello 值並貼到 hello**安全性憑證指紋**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="82a26-183">Copy hello **Thumbprint** value from hello downloaded certificate from Azure portal and paste it into hello **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="82a26-184">如需詳細資訊，請參閱[如何 tooretrieve 憑證的指紋值](http://youtu.be/YKQF266SAxI)。</span><span class="sxs-lookup"><span data-stu-id="82a26-184">For more details, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="82a26-185">f.</span><span class="sxs-lookup"><span data-stu-id="82a26-185">f.</span></span> <span data-ttu-id="82a26-186">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="82a26-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="82a26-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="82a26-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="82a26-188">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="82a26-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="82a26-190">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="82a26-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a26-191">在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="82a26-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="82a26-193">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="82a26-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="82a26-195">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="82a26-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="82a26-197">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="82a26-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="82a26-199">a.</span><span class="sxs-lookup"><span data-stu-id="82a26-199">a.</span></span> <span data-ttu-id="82a26-200">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="82a26-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82a26-201">b.</span><span class="sxs-lookup"><span data-stu-id="82a26-201">b.</span></span> <span data-ttu-id="82a26-202">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="82a26-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="82a26-203">c.</span><span class="sxs-lookup"><span data-stu-id="82a26-203">c.</span></span> <span data-ttu-id="82a26-204">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="82a26-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="82a26-205">d.</span><span class="sxs-lookup"><span data-stu-id="82a26-205">d.</span></span> <span data-ttu-id="82a26-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="82a26-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="82a26-207">建立 FreshDesk 測試使用者</span><span class="sxs-lookup"><span data-stu-id="82a26-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="82a26-208">在訂單 tooenable Azure AD 使用者 toolog 入 FreshDesk，它們必須佈建到 FreshDesk。</span><span class="sxs-lookup"><span data-stu-id="82a26-208">In order tooenable Azure AD users toolog into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="82a26-209">在 FreshDesk 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="82a26-209">In hello case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="82a26-210">**tooprovision 使用者帳戶，執行下列步驟 hello:**</span><span class="sxs-lookup"><span data-stu-id="82a26-210">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a26-211">登入 tooyour **Freshdesk**租用戶。</span><span class="sxs-lookup"><span data-stu-id="82a26-211">Log in tooyour **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="82a26-212">在 [hello 最上層顯示 hello 功能表上，按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="82a26-212">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="82a26-213">![管理](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "管理")</span><span class="sxs-lookup"><span data-stu-id="82a26-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="82a26-214">在 [hello**一般設定**索引標籤上，按一下 [**代理程式**。</span><span class="sxs-lookup"><span data-stu-id="82a26-214">In hello **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="82a26-215">![代理程式](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "代理程式")</span><span class="sxs-lookup"><span data-stu-id="82a26-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="82a26-216">按一下 [新增代理程式] 。</span><span class="sxs-lookup"><span data-stu-id="82a26-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="82a26-217">![新代理程式](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "新代理程式")</span><span class="sxs-lookup"><span data-stu-id="82a26-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="82a26-218">在 hello 代理程式資訊] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="82a26-218">On hello Agent Information dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="82a26-219">![代理程式資訊](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "代理程式資訊")</span><span class="sxs-lookup"><span data-stu-id="82a26-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="82a26-220">a.</span><span class="sxs-lookup"><span data-stu-id="82a26-220">a.</span></span> <span data-ttu-id="82a26-221">在 [hello**全名**文字方塊中，您想要讓 tooprovision 的 hello Azure AD 帳戶 hello 型別名稱。</span><span class="sxs-lookup"><span data-stu-id="82a26-221">In hello **Full Name** textbox, type hello name of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="82a26-222">b.</span><span class="sxs-lookup"><span data-stu-id="82a26-222">b.</span></span> <span data-ttu-id="82a26-223">在 [hello**電子郵件**文字方塊中，型別 hello Azure AD 電子郵件地址將要 hello Azure AD 帳戶 tooprovision。</span><span class="sxs-lookup"><span data-stu-id="82a26-223">In hello **Email** textbox, type hello Azure AD email address of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="82a26-224">c.</span><span class="sxs-lookup"><span data-stu-id="82a26-224">c.</span></span> <span data-ttu-id="82a26-225">在 [hello**標題**文字方塊中，您想 tooprovision 的 hello Azure AD 帳戶類型 hello 標題。</span><span class="sxs-lookup"><span data-stu-id="82a26-225">In hello **Title** textbox, type hello title of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="82a26-226">d.</span><span class="sxs-lookup"><span data-stu-id="82a26-226">d.</span></span> <span data-ttu-id="82a26-227">選取 [代理程式角色]，然後按一下 [指派]。</span><span class="sxs-lookup"><span data-stu-id="82a26-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="82a26-228">e.</span><span class="sxs-lookup"><span data-stu-id="82a26-228">e.</span></span> <span data-ttu-id="82a26-229">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="82a26-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="82a26-230">hello Azure AD 帳戶持有者會收到電子郵件，其中包含連結 tooconfirm hello 帳戶之前，它便啟動。</span><span class="sxs-lookup"><span data-stu-id="82a26-230">hello Azure AD account holder will get an email that includes a link tooconfirm hello account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="82a26-231">您可以使用任何其他 Freshdesk 使用者帳戶建立工具或 Api 提供 Freshdesk tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="82a26-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk tooprovision AAD user accounts.</span></span> <span data-ttu-id="82a26-232">tooFreshDesk。</span><span class="sxs-lookup"><span data-stu-id="82a26-232">tooFreshDesk.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="82a26-233">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="82a26-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="82a26-234">在本節中，您可以授與他們存取 tooBox 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="82a26-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBox.</span></span>

![指派使用者][200] 

<span data-ttu-id="82a26-236">**tooassign 許 Simon tooFreshDesk，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="82a26-236">**tooassign Britta Simon tooFreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a26-237">在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="82a26-237">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="82a26-239">在 [hello] 應用程式清單中，選取**FreshDesk**。</span><span class="sxs-lookup"><span data-stu-id="82a26-239">In hello applications list, select **FreshDesk**.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="82a26-241">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="82a26-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="82a26-243">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="82a26-243">Click **Add** button.</span></span> <span data-ttu-id="82a26-244">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="82a26-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="82a26-246">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="82a26-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="82a26-247">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="82a26-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="82a26-248">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="82a26-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="82a26-249">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="82a26-249">Testing single sign-on</span></span>

<span data-ttu-id="82a26-250">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="82a26-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="82a26-251">當您按一下 hello FreshDesk 磚 hello 存取面板中的時，您應該取得登入頁面 tooget 登入 tooyour FreshDesk 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="82a26-251">When you click hello FreshDesk tile in hello Access Panel, you should get login page tooget signed-on tooyour FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82a26-252">其他資源</span><span class="sxs-lookup"><span data-stu-id="82a26-252">Additional resources</span></span>

* [<span data-ttu-id="82a26-253">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82a26-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82a26-254">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="82a26-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

