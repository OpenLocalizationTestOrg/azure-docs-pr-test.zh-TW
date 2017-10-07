---
title: "教學課程：Azure Active Directory 與 SuccessFactors 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse SuccessFactors 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="f5796-103">教學課程：Azure Active Directory 與 SuccessFactors 整合</span><span class="sxs-lookup"><span data-stu-id="f5796-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="f5796-104">本教學課程的 hello 目標是 tooshow 您如何 toointegrate SuccessFactors 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="f5796-104">hello objective of this tutorial is tooshow you how toointegrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5796-105">與 Azure AD 整合 SuccessFactors 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="f5796-105">Integrating SuccessFactors with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="f5796-106">您可以控制存取 tooSuccessFactors Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="f5796-106">You can control in Azure AD who has access tooSuccessFactors</span></span>
* <span data-ttu-id="f5796-107">您可以啟用您的使用者 tooautomatically get 登入 tooSuccessFactors （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="f5796-107">You can enable your users tooautomatically get signed-on tooSuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="f5796-108">您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="f5796-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="f5796-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f5796-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5796-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f5796-110">Prerequisites</span></span>
<span data-ttu-id="f5796-111">tooconfigure 與 SuccessFactors 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="f5796-111">tooconfigure Azure AD integration with SuccessFactors, you need hello following items:</span></span>

* <span data-ttu-id="f5796-112">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="f5796-112">A valid Azure subscription</span></span>
* <span data-ttu-id="f5796-113">SuccessFactors 中的租用戶</span><span class="sxs-lookup"><span data-stu-id="f5796-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="f5796-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="f5796-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="f5796-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f5796-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="f5796-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="f5796-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="f5796-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f5796-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5796-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f5796-118">Scenario description</span></span>
<span data-ttu-id="f5796-119">本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 單一登入的測試環境中。</span><span class="sxs-lookup"><span data-stu-id="f5796-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="f5796-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="f5796-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5796-121">從 hello 圖庫加入 SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="f5796-121">Adding SuccessFactors from hello gallery</span></span>
2. <span data-ttu-id="f5796-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f5796-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-hello-gallery"></a><span data-ttu-id="f5796-123">從 hello 圖庫加入 SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="f5796-123">Adding SuccessFactors from hello gallery</span></span>
<span data-ttu-id="f5796-124">tooconfigure hello 整合 SuccessFactors 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SuccessFactors。</span><span class="sxs-lookup"><span data-stu-id="f5796-124">tooconfigure hello integration of SuccessFactors into Azure AD, you need tooadd SuccessFactors from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f5796-125">**tooadd SuccessFactors hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f5796-125">**tooadd SuccessFactors from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5796-126">在 hello Azure 傳統入口網站上 hello 左邊的導覽面板中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="f5796-126">In hello Azure classic portal, on hello left navigation panel, click **Active Directory**.</span></span>
   
    ![設定單一登入][1]
2. <span data-ttu-id="f5796-128">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="f5796-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="f5796-129">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="f5796-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![設定單一登入][2]
4. <span data-ttu-id="f5796-131">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="f5796-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![應用程式][3]
5. <span data-ttu-id="f5796-133">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f5796-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![設定單一登入][4]
6. <span data-ttu-id="f5796-135">在 hello**搜尋方塊**，型別**SuccessFactors**。</span><span class="sxs-lookup"><span data-stu-id="f5796-135">In hello **search box**, type **SuccessFactors**.</span></span>
   
    ![設定單一登入][5]
7. <span data-ttu-id="f5796-137">在 hello 結果 窗格中，選取  **SuccessFactors**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5796-137">In hello results panel, select **SuccessFactors**, and then click **Complete** tooadd hello application.</span></span>
   
    ![設定單一登入][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5796-139">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f5796-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5796-140">hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD 單一登入與 SuccessFactors 根據稱為 「 許 Simon"的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f5796-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f5796-141">單一登入 toowork，Azure AD 需要 tooknow 是在 SuccessFactors tooan 使用者在 Azure AD 中的 hello 對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="f5796-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SuccessFactors tooan user in Azure AD is.</span></span> <span data-ttu-id="f5796-142">換句話說，Azure AD 使用者與 hello SuccessFactors 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="f5796-142">In other words, a link relationship between an Azure AD user and hello related user in SuccessFactors needs toobe established.</span></span>

<span data-ttu-id="f5796-143">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** SuccessFactors 中。</span><span class="sxs-lookup"><span data-stu-id="f5796-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SuccessFactors.</span></span>

<span data-ttu-id="f5796-144">tooconfigure 及測試 Azure AD 單一登入 SuccessFactors，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="f5796-144">tooconfigure and test Azure AD single sign-on with SuccessFactors, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f5796-145">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="f5796-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f5796-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="f5796-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5796-147">**[建立測試使用者 SuccessFactors](#creating-a-successfactors-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 SuccessFactors 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="f5796-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - toohave a counterpart of Britta Simon in SuccessFactors that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="f5796-148">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5796-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5796-149">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="f5796-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5796-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f5796-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="f5796-151">在本節中，您可以啟用 Azure AD 單一登入 hello 傳統入口網站中，並設定單一登入 SuccessFactors 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="f5796-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="f5796-152">**tooconfigure Azure AD 單一登入 SuccessFactors 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f5796-152">**tooconfigure Azure AD single sign-on with SuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5796-153">在 Azure 傳統入口網站，在 hello hello **SuccessFactors**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f5796-153">In hello Azure classic portal, on hello **SuccessFactors** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    ![設定單一登入][7]
2. <span data-ttu-id="f5796-155">在 hello**如何想您使用者 toosign tooSuccessFactors 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f5796-155">On hello **How would you like users toosign on tooSuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![設定單一登入][8]
3. <span data-ttu-id="f5796-157">在 hello**設定應用程式 URL**頁面上，執行下列步驟，hello，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f5796-157">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    ![設定單一登入][9]
   
    <span data-ttu-id="f5796-159">a.</span><span class="sxs-lookup"><span data-stu-id="f5796-159">a.</span></span> <span data-ttu-id="f5796-160">在 hello**登入 URL**文字方塊中，輸入 URL，使用其中一個 hello 下列模式：</span><span class="sxs-lookup"><span data-stu-id="f5796-160">In hello **Sign On URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="f5796-161">b.</span><span class="sxs-lookup"><span data-stu-id="f5796-161">b.</span></span> <span data-ttu-id="f5796-162">在 hello**回覆 URL**文字方塊中，輸入 URL，使用其中一個 hello 下列模式：</span><span class="sxs-lookup"><span data-stu-id="f5796-162">In hello **Reply URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="f5796-163">c.</span><span class="sxs-lookup"><span data-stu-id="f5796-163">c.</span></span> <span data-ttu-id="f5796-164">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f5796-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="f5796-165">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="f5796-165">Please note that these are not hello real values.</span></span> <span data-ttu-id="f5796-166">您有 tooupdate hello 實際的登入 URL 及回覆 URL 與這些值。</span><span class="sxs-lookup"><span data-stu-id="f5796-166">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="f5796-167">tooget 這些值，請連絡[SuccessFactors 支援團隊](https://www.successfactors.com/en_us/support.html)。</span><span class="sxs-lookup"><span data-stu-id="f5796-167">tooget these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="f5796-168">在 hello**於 SuccessFactors 設定單一登入**頁面上，按一下**下載憑證**，然後儲存在本機電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="f5796-168">On hello **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![設定單一登入][10]

2. <span data-ttu-id="f5796-170">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **SuccessFactors 系統管理入口網站** 。</span><span class="sxs-lookup"><span data-stu-id="f5796-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="f5796-171">請瀏覽**應用程式安全性**和原生太**單一登入的功能**。</span><span class="sxs-lookup"><span data-stu-id="f5796-171">Visit **Application Security** and native too**Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="f5796-172">任何值置於 hello**重設語彙基元**按一下**語彙基元儲存**tooenable SAML SSO。</span><span class="sxs-lookup"><span data-stu-id="f5796-172">Place any value in hello **Reset Token** and click **Save Token** tooenable SAML SSO.</span></span>
   
    ![在應用程式端設定單一登入][11]

    > [!NOTE] 
    > <span data-ttu-id="f5796-174">這個值只做 hello 開啟/關閉參數。</span><span class="sxs-lookup"><span data-stu-id="f5796-174">This value is just used as hello on/off switch.</span></span> <span data-ttu-id="f5796-175">如果儲存的任何值，hello SAML SSO 會是 ON。</span><span class="sxs-lookup"><span data-stu-id="f5796-175">If any value is saved, hello SAML SSO is ON.</span></span> <span data-ttu-id="f5796-176">如果為空白值會儲存 hello SAML SSO 為 OFF。</span><span class="sxs-lookup"><span data-stu-id="f5796-176">If a blank value is saved hello SAML SSO is OFF.</span></span>

1. <span data-ttu-id="f5796-177">原生 toobelow 螢幕擷取畫面，並執行下列動作的 hello。</span><span class="sxs-lookup"><span data-stu-id="f5796-177">Native toobelow screenshot and perform hello following actions.</span></span>
   
    ![在應用程式端設定單一登入][12]
   
    <span data-ttu-id="f5796-179">a.</span><span class="sxs-lookup"><span data-stu-id="f5796-179">a.</span></span> <span data-ttu-id="f5796-180">選取 hello **SAML v2 SSO**選項按鈕</span><span class="sxs-lookup"><span data-stu-id="f5796-180">Select hello **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="f5796-181">b.</span><span class="sxs-lookup"><span data-stu-id="f5796-181">b.</span></span> <span data-ttu-id="f5796-182">設定 SAML 判斷提示的合作對象 Name(e.g.SAml issuer + company name) hello。</span><span class="sxs-lookup"><span data-stu-id="f5796-182">Set hello SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="f5796-183">c.</span><span class="sxs-lookup"><span data-stu-id="f5796-183">c.</span></span> <span data-ttu-id="f5796-184">在 hello **SAML 簽發者**文字方塊放 hello 值**簽發者 URL**從 Azure AD 應用程式組態精靈。</span><span class="sxs-lookup"><span data-stu-id="f5796-184">In hello **SAML Issuer** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="f5796-185">d.</span><span class="sxs-lookup"><span data-stu-id="f5796-185">d.</span></span> <span data-ttu-id="f5796-186">選取 [回應 (客戶產生的/IdP/AP)] 做為 [需要必要簽章]。</span><span class="sxs-lookup"><span data-stu-id="f5796-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="f5796-187">e.</span><span class="sxs-lookup"><span data-stu-id="f5796-187">e.</span></span> <span data-ttu-id="f5796-188">選取 [啟用] 做為 [啟用 SAML 旗標]。</span><span class="sxs-lookup"><span data-stu-id="f5796-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="f5796-189">f.</span><span class="sxs-lookup"><span data-stu-id="f5796-189">f.</span></span> <span data-ttu-id="f5796-190">選取 [否] 做為 [登入要求簽章 (SF 產生的/SP/RP)]。</span><span class="sxs-lookup"><span data-stu-id="f5796-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="f5796-191">g.</span><span class="sxs-lookup"><span data-stu-id="f5796-191">g.</span></span> <span data-ttu-id="f5796-192">選取 [瀏覽器/後置設定檔] 做為 [SAML 設定檔]。</span><span class="sxs-lookup"><span data-stu-id="f5796-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="f5796-193">h.</span><span class="sxs-lookup"><span data-stu-id="f5796-193">h.</span></span> <span data-ttu-id="f5796-194">選取 [否] 做為 [強制執行憑證有效期間]。</span><span class="sxs-lookup"><span data-stu-id="f5796-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="f5796-195">i.</span><span class="sxs-lookup"><span data-stu-id="f5796-195">i.</span></span> <span data-ttu-id="f5796-196">Hello hello 下載的憑證檔案的內容複製並貼到 hello **SAML 驗證憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="f5796-196">Copy hello content of hello downloaded certificate file, and then paste it into hello **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f5796-197">hello 憑證內容必須有憑證和結束憑證標記開頭。</span><span class="sxs-lookup"><span data-stu-id="f5796-197">hello certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="f5796-198">瀏覽 tooSAML V2、，然後執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f5796-198">Navigate tooSAML V2, and then perform hello following steps:</span></span>
   
    ![在應用程式端設定單一登入][13]
   
    <span data-ttu-id="f5796-200">a.</span><span class="sxs-lookup"><span data-stu-id="f5796-200">a.</span></span> <span data-ttu-id="f5796-201">選取 [是] 做為 [支援 SP 起始的全域登出]。</span><span class="sxs-lookup"><span data-stu-id="f5796-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="f5796-202">b.</span><span class="sxs-lookup"><span data-stu-id="f5796-202">b.</span></span> <span data-ttu-id="f5796-203">在 hello**全域登出服務 URL （LogoutRequest 目的地）**文字方塊放 hello 值**遠端登出 URL**從 Azure AD 應用程式組態精靈。</span><span class="sxs-lookup"><span data-stu-id="f5796-203">In hello **Global Logout Service URL (LogoutRequest destination)** textbox put hello value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="f5796-204">c.</span><span class="sxs-lookup"><span data-stu-id="f5796-204">c.</span></span> <span data-ttu-id="f5796-205">選取 [否] 做為 [要求 SP 必須加密所有 NameID 元素]。</span><span class="sxs-lookup"><span data-stu-id="f5796-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="f5796-206">d.</span><span class="sxs-lookup"><span data-stu-id="f5796-206">d.</span></span> <span data-ttu-id="f5796-207">選取 [未指定] 做為 [NameID 格式]。</span><span class="sxs-lookup"><span data-stu-id="f5796-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="f5796-208">e.</span><span class="sxs-lookup"><span data-stu-id="f5796-208">e.</span></span> <span data-ttu-id="f5796-209">選取 [是] 做為 [啟用 SP 起始的登入 (AuthnRequest)]。</span><span class="sxs-lookup"><span data-stu-id="f5796-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="f5796-210">f.</span><span class="sxs-lookup"><span data-stu-id="f5796-210">f.</span></span> <span data-ttu-id="f5796-211">在 hello**做全公司的簽發者傳送要求**文字方塊放 hello 值**遠端登入 URL**從 Azure AD 應用程式組態精靈。</span><span class="sxs-lookup"><span data-stu-id="f5796-211">In hello **Send request as Company-Wide issuer** textbox put hello value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="f5796-212">執行這些步驟，如果您想 toomake hello 登入使用者名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="f5796-212">Perform these steps if you want toomake hello login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="f5796-213">a.</span><span class="sxs-lookup"><span data-stu-id="f5796-213">a.</span></span> <span data-ttu-id="f5796-214">請瀏覽**公司設定**(near hello 下方）。</span><span class="sxs-lookup"><span data-stu-id="f5796-214">Visit **Company Settings**(near hello bottom).</span></span>
   
    <span data-ttu-id="f5796-215">b.</span><span class="sxs-lookup"><span data-stu-id="f5796-215">b.</span></span> <span data-ttu-id="f5796-216">選取 [啟用不區分大小寫使用者名稱] 附近的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f5796-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="f5796-217">c. 按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f5796-217">c.Click **Save**.</span></span>
   
    ![設定單一登入][29]

    > [!NOTE] 
    > <span data-ttu-id="f5796-219">如果您嘗試 tooenable，hello 系統會檢查如果網域控制站會建立重複的 SAML 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="f5796-219">If you try tooenable this, hello system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="f5796-220">例如，如果 hello 客戶有 User1 和 user1 的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f5796-220">For example if hello customer has usernames User1 and user1.</span></span> <span data-ttu-id="f5796-221">取消區分大小寫功能將會讓這些名稱重複。</span><span class="sxs-lookup"><span data-stu-id="f5796-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="f5796-222">hello 系統提供的錯誤訊息，並將不會啟用 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="f5796-222">hello system will give you an error message and will not enable hello feature.</span></span> <span data-ttu-id="f5796-223">hello 客戶將會需要 toochange hello 使用者名稱的其中一個，實際的拼法不同。</span><span class="sxs-lookup"><span data-stu-id="f5796-223">hello customer will need toochange one of hello usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="f5796-224">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f5796-224">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    ![應用程式][14]
2. <span data-ttu-id="f5796-226">在 hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="f5796-226">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![應用程式][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5796-228">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f5796-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5796-229">本節 hello 目標是 toocreate 測試使用者呼叫許 Simon hello 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="f5796-229">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][16]

<span data-ttu-id="f5796-231">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f5796-231">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5796-232">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="f5796-232">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者][17]
2. <span data-ttu-id="f5796-234">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="f5796-234">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="f5796-235">toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="f5796-235">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者][18]
4. <span data-ttu-id="f5796-237">tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="f5796-237">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![建立 Azure AD 測試使用者][19]
5. <span data-ttu-id="f5796-239">在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f5796-239">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者][20]
   
    <span data-ttu-id="f5796-241">a.</span><span class="sxs-lookup"><span data-stu-id="f5796-241">a.</span></span> <span data-ttu-id="f5796-242">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="f5796-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="f5796-243">b.</span><span class="sxs-lookup"><span data-stu-id="f5796-243">b.</span></span> <span data-ttu-id="f5796-244">在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f5796-244">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="f5796-245">c.</span><span class="sxs-lookup"><span data-stu-id="f5796-245">c.</span></span> <span data-ttu-id="f5796-246">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f5796-246">Click **Next**.</span></span>
6. <span data-ttu-id="f5796-247">在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f5796-247">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者][21]
   
    <span data-ttu-id="f5796-249">a.</span><span class="sxs-lookup"><span data-stu-id="f5796-249">a.</span></span> <span data-ttu-id="f5796-250">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="f5796-250">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="f5796-251">b.</span><span class="sxs-lookup"><span data-stu-id="f5796-251">b.</span></span> <span data-ttu-id="f5796-252">在 hello**姓氏**文字方塊中，輸入， **Simon**。</span><span class="sxs-lookup"><span data-stu-id="f5796-252">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="f5796-253">c.</span><span class="sxs-lookup"><span data-stu-id="f5796-253">c.</span></span> <span data-ttu-id="f5796-254">在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="f5796-254">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="f5796-255">d.</span><span class="sxs-lookup"><span data-stu-id="f5796-255">d.</span></span> <span data-ttu-id="f5796-256">在 hello**角色**清單中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="f5796-256">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="f5796-257">e.</span><span class="sxs-lookup"><span data-stu-id="f5796-257">e.</span></span> <span data-ttu-id="f5796-258">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f5796-258">Click **Next**.</span></span>
7. <span data-ttu-id="f5796-259">在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="f5796-259">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者][22]
8. <span data-ttu-id="f5796-261">在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f5796-261">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者][23]
   
    <span data-ttu-id="f5796-263">a.</span><span class="sxs-lookup"><span data-stu-id="f5796-263">a.</span></span> <span data-ttu-id="f5796-264">請記下 hello hello 值**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="f5796-264">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="f5796-265">b.</span><span class="sxs-lookup"><span data-stu-id="f5796-265">b.</span></span> <span data-ttu-id="f5796-266">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f5796-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="f5796-267">建立 SuccessFactors 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f5796-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="f5796-268">在訂單 tooenable Azure AD 使用者 toolog 入 SuccessFactors，它們必須佈建到 SuccessFactors。</span><span class="sxs-lookup"><span data-stu-id="f5796-268">In order tooenable Azure AD users toolog into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="f5796-269">在 SuccessFactors 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="f5796-269">In hello case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="f5796-270">tooget SuccessFactors 中建立的使用者，您需要 toocontact hello [SuccessFactors 支援團隊](https://www.successfactors.com/en_us/support.html)。</span><span class="sxs-lookup"><span data-stu-id="f5796-270">tooget users created in SuccessFactors, you need toocontact hello [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f5796-271">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="f5796-271">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="f5796-272">本節 hello 目標是授與他們存取 tooSuccessFactors tooenabling 許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5796-272">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSuccessFactors.</span></span>

![指派使用者][24]

<span data-ttu-id="f5796-274">**tooassign 許 Simon tooSuccessFactors，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f5796-274">**tooassign Britta Simon tooSuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5796-275">Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="f5796-275">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![指派使用者][25]
2. <span data-ttu-id="f5796-277">在 [hello] 應用程式清單中，選取**SuccessFactors**。</span><span class="sxs-lookup"><span data-stu-id="f5796-277">In hello applications list, select **SuccessFactors**.</span></span>
   
    ![設定單一登入][26]
3. <span data-ttu-id="f5796-279">在 hello 最上層顯示 hello 功能表上，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="f5796-279">In hello menu on hello top, click **Users**.</span></span>
   
    ![指派使用者][27]
4. <span data-ttu-id="f5796-281">在 hello 使用者清單中選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="f5796-281">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="f5796-282">在 hello hello 底部的工具列中按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="f5796-282">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![指派使用者][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="f5796-284">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f5796-284">Testing single sign-on</span></span>
<span data-ttu-id="f5796-285">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="f5796-285">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f5796-286">當您按一下的 hello SuccessFactors 磚 hello 存取面板中時，您應該取得自動登入 tooyour SuccessFactors 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5796-286">When you click hello SuccessFactors tile in hello Access Panel, you should get automatically signed-on tooyour SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5796-287">其他資源</span><span class="sxs-lookup"><span data-stu-id="f5796-287">Additional resources</span></span>
* [<span data-ttu-id="f5796-288">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5796-288">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5796-289">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f5796-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
