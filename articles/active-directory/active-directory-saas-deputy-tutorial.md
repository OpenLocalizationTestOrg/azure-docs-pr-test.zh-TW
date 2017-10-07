---
title: "教學課程：Azure Active Directory 與 Deputy 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 和副之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="9fbad-103">教學課程：Azure Active Directory 與 Deputy 整合</span><span class="sxs-lookup"><span data-stu-id="9fbad-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="9fbad-104">在此教學課程中，您學會如何 toointegrate 副與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="9fbad-104">In this tutorial, you learn how toointegrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9fbad-105">與 Azure AD 整合副可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="9fbad-105">Integrating Deputy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9fbad-106">您可以控制存取 tooDeputy Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="9fbad-106">You can control in Azure AD who has access tooDeputy</span></span>
- <span data-ttu-id="9fbad-107">您可以啟用您的使用者 tooautomatically get 登入 tooDeputy （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="9fbad-107">You can enable your users tooautomatically get signed-on tooDeputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9fbad-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9fbad-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9fbad-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9fbad-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fbad-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9fbad-110">Prerequisites</span></span>

<span data-ttu-id="9fbad-111">tooconfigure 副與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="9fbad-111">tooconfigure Azure AD integration with Deputy, you need hello following items:</span></span>

- <span data-ttu-id="9fbad-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9fbad-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9fbad-113">已啟用 Deputy 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9fbad-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9fbad-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="9fbad-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9fbad-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="9fbad-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9fbad-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9fbad-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9fbad-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="9fbad-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9fbad-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9fbad-118">Scenario description</span></span>
<span data-ttu-id="9fbad-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9fbad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9fbad-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="9fbad-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9fbad-121">從 hello 圖庫加入副</span><span class="sxs-lookup"><span data-stu-id="9fbad-121">Adding Deputy from hello gallery</span></span>
2. <span data-ttu-id="9fbad-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9fbad-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-hello-gallery"></a><span data-ttu-id="9fbad-123">從 hello 圖庫加入副</span><span class="sxs-lookup"><span data-stu-id="9fbad-123">Adding Deputy from hello gallery</span></span>
<span data-ttu-id="9fbad-124">tooconfigure hello 整合副到 Azure AD，您需要 tooadd 副 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9fbad-124">tooconfigure hello integration of Deputy into Azure AD, you need tooadd Deputy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9fbad-125">**tooadd 副 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9fbad-125">**tooadd Deputy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fbad-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9fbad-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9fbad-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9fbad-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="9fbad-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9fbad-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="9fbad-133">在 [hello] 搜尋方塊中，輸入**副**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-133">In hello search box, type **Deputy**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="9fbad-135">在 hello 結果 窗格中，選取 **副**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9fbad-135">In hello results panel, select **Deputy**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9fbad-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9fbad-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9fbad-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Deputy 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9fbad-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9fbad-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中副是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="9fbad-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Deputy is tooa user in Azure AD.</span></span> <span data-ttu-id="9fbad-140">換句話說，Azure AD 使用者與 hello 副中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="9fbad-140">In other words, a link relationship between an Azure AD user and hello related user in Deputy needs toobe established.</span></span>

<span data-ttu-id="9fbad-141">副中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9fbad-141">In Deputy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9fbad-142">tooconfigure 及副與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="9fbad-142">tooconfigure and test Azure AD single sign-on with Deputy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9fbad-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="9fbad-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9fbad-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="9fbad-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9fbad-145">**[建立測試使用者副](#creating-a-deputy-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的副中對應項目。</span><span class="sxs-lookup"><span data-stu-id="9fbad-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - toohave a counterpart of Britta Simon in Deputy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9fbad-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9fbad-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9fbad-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="9fbad-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9fbad-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9fbad-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9fbad-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並副應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="9fbad-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="9fbad-150">**tooconfigure Azure AD 單一登入與副，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9fbad-150">**tooconfigure Azure AD single sign-on with Deputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fbad-151">在 Azure 入口網站上 hello hello**副**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-151">In hello Azure portal, on hello **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="9fbad-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9fbad-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="9fbad-155">在 hello**副網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="9fbad-155">On hello **Deputy Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="9fbad-157">a.</span><span class="sxs-lookup"><span data-stu-id="9fbad-157">a.</span></span> <span data-ttu-id="9fbad-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="9fbad-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="9fbad-159">b.</span><span class="sxs-lookup"><span data-stu-id="9fbad-159">b.</span></span> <span data-ttu-id="9fbad-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="9fbad-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="9fbad-161">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="9fbad-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="9fbad-162">如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="9fbad-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="9fbad-164">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="9fbad-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="9fbad-165">Deputy 區域尾碼是選擇性的，或者應該使用下列其中一個︰au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span><span class="sxs-lookup"><span data-stu-id="9fbad-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9fbad-166">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="9fbad-166">These values are not real.</span></span> <span data-ttu-id="9fbad-167">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="9fbad-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9fbad-168">請連絡[副支援小組](https://www.deputy.com/call-centers-customer-support-scheduling-software)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="9fbad-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget these values.</span></span> 

5. <span data-ttu-id="9fbad-169">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="9fbad-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="9fbad-171">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9fbad-171">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9fbad-173">在 hello**副組態**區段中，按一下**設定副**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="9fbad-173">On hello **Deputy Configuration** section, click **Configure Deputy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9fbad-174">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="9fbad-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="9fbad-176">瀏覽下列 URL toohello:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config)。</span><span class="sxs-lookup"><span data-stu-id="9fbad-176">Navigate toohello following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="9fbad-177">跳過**安全性設定**按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-177">Go too**Security Settings** and click **Edit**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="9fbad-179">在此 [安全性設定]  頁面上，執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="9fbad-179">On this **Security Settings** page, perform below steps.</span></span>

    ![設定單一登入](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="9fbad-181">a.</span><span class="sxs-lookup"><span data-stu-id="9fbad-181">a.</span></span> <span data-ttu-id="9fbad-182">啟用**社交登入**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="9fbad-183">b.</span><span class="sxs-lookup"><span data-stu-id="9fbad-183">b.</span></span> <span data-ttu-id="9fbad-184">開啟 [記事本]，複製到剪貼簿，其內容的 hello Azure 入口網站從下載的 Base64 編碼憑證，然後將它貼入 toohello **OpenSSL 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="9fbad-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="9fbad-185">c.</span><span class="sxs-lookup"><span data-stu-id="9fbad-185">c.</span></span> <span data-ttu-id="9fbad-186">在 [hello SAML SSO URL] 文字方塊中，輸入`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="9fbad-186">In hello SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="9fbad-187">d.</span><span class="sxs-lookup"><span data-stu-id="9fbad-187">d.</span></span> <span data-ttu-id="9fbad-188">在 [hello SAML SSO URL] 文字方塊中，取代`<your subdomain>`與您的子網域。</span><span class="sxs-lookup"><span data-stu-id="9fbad-188">In hello SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="9fbad-189">e.</span><span class="sxs-lookup"><span data-stu-id="9fbad-189">e.</span></span> <span data-ttu-id="9fbad-190">在 [hello SAML SSO URL] 文字方塊中，取代`<saml sso url>`以 hello **SAML 單一登入服務 URL**從 hello Azure 入口網站複製。</span><span class="sxs-lookup"><span data-stu-id="9fbad-190">In hello SAML SSO URL textbox, replace `<saml sso url>` with hello **SAML Single Sign-On Service URL** you have copied from hello Azure portal.</span></span>
   
    <span data-ttu-id="9fbad-191">f.</span><span class="sxs-lookup"><span data-stu-id="9fbad-191">f.</span></span> <span data-ttu-id="9fbad-192">按一下 [儲存設定] 。</span><span class="sxs-lookup"><span data-stu-id="9fbad-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="9fbad-193">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="9fbad-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9fbad-194">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="9fbad-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9fbad-195">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9fbad-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9fbad-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9fbad-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="9fbad-197">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9fbad-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="9fbad-199">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9fbad-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fbad-200">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9fbad-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9fbad-202">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9fbad-204">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="9fbad-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9fbad-206">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9fbad-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9fbad-208">a.</span><span class="sxs-lookup"><span data-stu-id="9fbad-208">a.</span></span> <span data-ttu-id="9fbad-209">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9fbad-210">b.</span><span class="sxs-lookup"><span data-stu-id="9fbad-210">b.</span></span> <span data-ttu-id="9fbad-211">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="9fbad-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9fbad-212">c.</span><span class="sxs-lookup"><span data-stu-id="9fbad-212">c.</span></span> <span data-ttu-id="9fbad-213">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9fbad-214">d.</span><span class="sxs-lookup"><span data-stu-id="9fbad-214">d.</span></span> <span data-ttu-id="9fbad-215">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9fbad-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="9fbad-216">建立 Deputy 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9fbad-216">Creating a Deputy test user</span></span>

<span data-ttu-id="9fbad-217">tooenable Azure AD 使用者 toolog 中 tooDeputy，它們必須佈建到副。</span><span class="sxs-lookup"><span data-stu-id="9fbad-217">tooenable Azure AD users toolog in tooDeputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="9fbad-218">Deputy 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="9fbad-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="9fbad-219">tooprovision 使用者帳戶，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9fbad-219">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="9fbad-220">系統管理員身分登入 tooyour 副公司網站。</span><span class="sxs-lookup"><span data-stu-id="9fbad-220">Log in tooyour Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="9fbad-221">在 hello 上方導覽窗格中，按一下 **人員**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-221">On hello top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="9fbad-222">![人員](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "人員")</span><span class="sxs-lookup"><span data-stu-id="9fbad-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="9fbad-223">按一下 hello**加入人員**按鈕，然後按一下**新增單一人員**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-223">Click hello **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="9fbad-224">![新增人員](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "新增人員")</span><span class="sxs-lookup"><span data-stu-id="9fbad-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="9fbad-225">執行下列步驟的 hello 和按一下**儲存並邀請**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-225">Perform hello following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="9fbad-226">![新增使用者](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="9fbad-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="9fbad-227">a.</span><span class="sxs-lookup"><span data-stu-id="9fbad-227">a.</span></span> <span data-ttu-id="9fbad-228">在 hello**名稱**文字方塊中，型別名稱類似的 hello 使用者**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-228">In hello **Name** textbox, type name of hello user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="9fbad-229">b.</span><span class="sxs-lookup"><span data-stu-id="9fbad-229">b.</span></span> <span data-ttu-id="9fbad-230">在 hello**電子郵件**文字方塊中，您想要讓 tooprovision Azure AD 帳戶類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="9fbad-230">In hello **Email** textbox, type hello email address of an Azure AD account you want tooprovision.</span></span>
   
   <span data-ttu-id="9fbad-231">c.</span><span class="sxs-lookup"><span data-stu-id="9fbad-231">c.</span></span> <span data-ttu-id="9fbad-232">在 hello**在工作**文字方塊中，型別 hello 的商務名稱。</span><span class="sxs-lookup"><span data-stu-id="9fbad-232">In hello **Work at** textbox, type hello business name.</span></span>
   
   <span data-ttu-id="9fbad-233">d.</span><span class="sxs-lookup"><span data-stu-id="9fbad-233">d.</span></span> <span data-ttu-id="9fbad-234">按一下 [儲存並邀請] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9fbad-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="9fbad-235">hello AAD 帳戶持有者會收到一封電子郵件，並且遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="9fbad-235">hello AAD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="9fbad-236">您可以使用任何其他副使用者帳戶建立工具或 Api 提供副 tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="9fbad-236">You can use any other Deputy user account creation tools or APIs provided by Deputy tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9fbad-237">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="9fbad-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9fbad-238">在本節中，您可以授與存取 tooDeputy 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9fbad-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDeputy.</span></span>

![指派使用者][200] 

<span data-ttu-id="9fbad-240">**tooassign 許 Simon tooDeputy，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9fbad-240">**tooassign Britta Simon tooDeputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fbad-241">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9fbad-243">在 [hello] 應用程式清單中，選取**副**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-243">In hello applications list, select **Deputy**.</span></span>

    ![設定單一登入](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="9fbad-245">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="9fbad-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="9fbad-247">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9fbad-247">Click **Add** button.</span></span> <span data-ttu-id="9fbad-248">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9fbad-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="9fbad-250">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="9fbad-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9fbad-251">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9fbad-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9fbad-252">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9fbad-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9fbad-253">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9fbad-253">Testing single sign-on</span></span>

<span data-ttu-id="9fbad-254">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="9fbad-254">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="9fbad-255">當您按一下的 hello 副磚 hello 存取面板中時，您應該取得自動登入 tooyour 副應用程式。</span><span class="sxs-lookup"><span data-stu-id="9fbad-255">When you click hello Deputy tile in hello Access Panel, you should get automatically signed-on tooyour Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9fbad-256">其他資源</span><span class="sxs-lookup"><span data-stu-id="9fbad-256">Additional resources</span></span>

* [<span data-ttu-id="9fbad-257">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fbad-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9fbad-258">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9fbad-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

