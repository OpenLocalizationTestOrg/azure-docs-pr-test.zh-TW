---
title: "教學課程：Azure Active Directory 與 Questetra BPM Suite 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Questetra BPM 套件之間。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="de392-103">教學課程：Azure Active Directory 與 Questetra BPM Suite 整合</span><span class="sxs-lookup"><span data-stu-id="de392-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="de392-104">本教學課程的 hello 目標是 tooshow 您如何 toointegrate Questetra BPM Suite 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="de392-104">hello objective of this tutorial is tooshow you how toointegrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="de392-105">與 Azure AD 整合 Questetra BPM 套件可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="de392-105">Integrating Questetra BPM Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="de392-106">您可以控制存取 tooQuestetra BPM 套件的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="de392-106">You can control in Azure AD who has access tooQuestetra BPM Suite</span></span> 
* <span data-ttu-id="de392-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooQuestetra BPM 套件 （單一登入）</span><span class="sxs-lookup"><span data-stu-id="de392-107">You can enable your users tooautomatically get signed-on tooQuestetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="de392-108">您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="de392-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="de392-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="de392-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de392-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="de392-110">Prerequisites</span></span>
<span data-ttu-id="de392-111">tooconfigure Questetra BPM Suite 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="de392-111">tooconfigure Azure AD integration with Questetra BPM Suite, you need hello following items:</span></span>

* <span data-ttu-id="de392-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="de392-112">An Azure AD subscription</span></span>
* <span data-ttu-id="de392-113">已啟用 [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="de392-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de392-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="de392-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="de392-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="de392-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="de392-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="de392-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="de392-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="de392-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="de392-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="de392-118">Scenario Description</span></span>
<span data-ttu-id="de392-119">本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 單一登入的測試環境中。</span><span class="sxs-lookup"><span data-stu-id="de392-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="de392-120">本教學課程所述的 hello 案例包含三個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="de392-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="de392-121">從 hello 圖庫加入 Questetra BPM 套件</span><span class="sxs-lookup"><span data-stu-id="de392-121">Adding Questetra BPM Suite from hello gallery</span></span> 
2. <span data-ttu-id="de392-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de392-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a><span data-ttu-id="de392-123">從 hello 圖庫加入 Questetra BPM 套件</span><span class="sxs-lookup"><span data-stu-id="de392-123">Adding Questetra BPM Suite from hello gallery</span></span>
<span data-ttu-id="de392-124">tooconfigure hello 整合 Questetra BPM 套件到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Questetra BPM 套件。</span><span class="sxs-lookup"><span data-stu-id="de392-124">tooconfigure hello integration of Questetra BPM Suite into Azure AD, you need tooadd Questetra BPM Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="de392-125">**tooadd Questetra BPM 套件從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de392-125">**tooadd Questetra BPM Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="de392-126">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="de392-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="de392-128">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="de392-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="de392-129">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="de392-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![應用程式][2]

4. <span data-ttu-id="de392-131">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="de392-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![應用程式][3]

5. <span data-ttu-id="de392-133">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="de392-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![應用程式][4]

6. <span data-ttu-id="de392-135">在 [hello] 搜尋方塊中，輸入**Questetra BPM 套件**。</span><span class="sxs-lookup"><span data-stu-id="de392-135">In hello search box, type **Questetra BPM Suite**.</span></span>
   
    ![應用程式][5]

7. <span data-ttu-id="de392-137">在 hello 結果窗格中，選取  **Questetra BPM 套件**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="de392-137">In hello results pane, select **Questetra BPM Suite**, and then click **Complete** tooadd hello application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de392-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de392-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de392-139">hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD 單一登入與 Questetra BPM 套件根據稱為 「 許 Simon"的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="de392-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de392-140">單一登入 toowork，Azure AD 需要 tooknow Questetra BPM 套件 tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="de392-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Questetra BPM Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="de392-141">換句話說，Azure AD 使用者與 hello Questetra BPM 套件中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="de392-141">In other words, a link relationship between an Azure AD user and hello related user in Questetra BPM Suite needs toobe established.</span></span>  
<span data-ttu-id="de392-142">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Questetra BPM 套件中。</span><span class="sxs-lookup"><span data-stu-id="de392-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="de392-143">tooconfigure 及 Questetra BPM Suite 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="de392-143">tooconfigure and test Azure AD single sign-on with Questetra BPM Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="de392-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="de392-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="de392-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="de392-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de392-146">**[建立 Questetra BPM 套件的測試使用者](#creating-a-questetra-bpm-suite-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Questetra BPM 套件中的對應項目。</span><span class="sxs-lookup"><span data-stu-id="de392-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - toohave a counterpart of Britta Simon in Questetra BPM Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="de392-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de392-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de392-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="de392-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de392-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de392-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="de392-150">本節 hello 目標是 tooenable Azure AD 單一登入 Azure 傳統入口網站 hello 和 tooconfigure 單一登入 Questetra BPM Suite 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="de392-150">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="de392-151">**利用 Questetra BPM Suite，Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="de392-151">**tooconfigure Azure AD single sign-on with Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="de392-152">在 Azure 傳統入口網站，在 hello hello **Questetra BPM 套件**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="de392-152">In hello Azure classic portal, on hello **Questetra BPM Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][8]

2. <span data-ttu-id="de392-154">Hello 上**如何想您 tooQuestetra BPM 套件上的使用者 toosign**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="de392-154">On hello **How would you like users toosign on tooQuestetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][9]

3. <span data-ttu-id="de392-156">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 **Questetra BPM Suite** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="de392-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="de392-157">在 hello 最上層顯示 hello 功能表上，按一下**系統設定**。</span><span class="sxs-lookup"><span data-stu-id="de392-157">In hello menu on hello top, click **System Settings**.</span></span> 
   
    ![Azure AD 單一登入][10]

5. <span data-ttu-id="de392-159">tooopen hello **SingleSignOnSAML**頁面上，按一下**SSO (SAML)**。</span><span class="sxs-lookup"><span data-stu-id="de392-159">tooopen hello **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD 單一登入][11]

6. <span data-ttu-id="de392-161">在 Azure 傳統入口網站，在 hello hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="de392-161">In hello Azure classic portal, on hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![設定 App 設定][13]
   
    <span data-ttu-id="de392-163">a.</span><span class="sxs-lookup"><span data-stu-id="de392-163">a.</span></span> <span data-ttu-id="de392-164">在您**Questetra BPM 套件**hello 預存程序資訊 」 一節中的公司網站中，複製 hello **ACS URL**，然後將它貼入 hello**登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="de392-164">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="de392-165">b.</span><span class="sxs-lookup"><span data-stu-id="de392-165">b.</span></span> <span data-ttu-id="de392-166">在您**Questetra BPM 套件**hello 預存程序資訊 」 一節中的公司網站中，複製 hello**實體識別碼**，然後將它貼入 hello**簽發者 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="de392-166">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **Entity ID**, and then paste it into hello **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="de392-167">c.</span><span class="sxs-lookup"><span data-stu-id="de392-167">c.</span></span> <span data-ttu-id="de392-168">在您**Questetra BPM 套件**hello 預存程序資訊 」 一節中的公司網站中，複製 hello **ACS URL**，然後將它貼入 hello**回覆 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="de392-168">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="de392-169">d.</span><span class="sxs-lookup"><span data-stu-id="de392-169">d.</span></span> <span data-ttu-id="de392-170">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="de392-170">Click **Next**.</span></span>

7. <span data-ttu-id="de392-171">在 hello **Questetra BPM 套件在設定單一登入**頁面上，按一下**下載憑證**，然後儲存在本機電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="de392-171">On hello **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![設定單一登入][14]

8. <span data-ttu-id="de392-173">在您**Questetra BPM 套件**公司網站中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="de392-173">On you **Questetra BPM Suite** company site, perform hello following steps:</span></span> 
   
    ![設定單一登入][15]
   
    <span data-ttu-id="de392-175">a.</span><span class="sxs-lookup"><span data-stu-id="de392-175">a.</span></span> <span data-ttu-id="de392-176">選取 [啟用單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="de392-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="de392-177">b.</span><span class="sxs-lookup"><span data-stu-id="de392-177">b.</span></span> <span data-ttu-id="de392-178">在 hello Azure 傳統入口網站中，複製 hello**簽發者 URL**值並貼到 hello**實體識別碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="de392-178">On hello Azure classic portal, copy hello **Issuer URL** value, and then paste it into hello **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="de392-179">c.</span><span class="sxs-lookup"><span data-stu-id="de392-179">c.</span></span> <span data-ttu-id="de392-180">在 hello Azure 傳統入口網站中，複製 hello**單一登入服務 URL**值並貼到 hello**登入頁面 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="de392-180">On hello Azure classic portal, copy hello **Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="de392-181">d.</span><span class="sxs-lookup"><span data-stu-id="de392-181">d.</span></span> <span data-ttu-id="de392-182">在 hello Azure 傳統入口網站中，複製 hello**單一登出服務 URL**值並貼到 hello**登出頁面 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="de392-182">On hello Azure classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="de392-183">e.</span><span class="sxs-lookup"><span data-stu-id="de392-183">e.</span></span> <span data-ttu-id="de392-184">在 hello **NameID 格式**文字方塊中，輸入**urn: oasis： 名稱： tc: saml: 1.1 nameid-format-: emailAddress**。</span><span class="sxs-lookup"><span data-stu-id="de392-184">In hello **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="de392-185">f.</span><span class="sxs-lookup"><span data-stu-id="de392-185">f.</span></span> <span data-ttu-id="de392-186">從您下載的憑證建立 Base-64 編碼檔案。</span><span class="sxs-lookup"><span data-stu-id="de392-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="de392-187">如需詳細資訊，請參閱[如何 tooconvert 二進位憑證到文字檔](http://youtu.be/PlgrzUZ-Y1o)。</span><span class="sxs-lookup"><span data-stu-id="de392-187">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="de392-188">g.</span><span class="sxs-lookup"><span data-stu-id="de392-188">g.</span></span> <span data-ttu-id="de392-189">[記事本]，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後將它貼到 hello**驗證憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="de392-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="de392-190">h.</span><span class="sxs-lookup"><span data-stu-id="de392-190">h.</span></span> <span data-ttu-id="de392-191">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="de392-191">Click **Save**.</span></span>

1. <span data-ttu-id="de392-192">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="de392-192">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![何謂 Azure AD Connect][17]

2. <span data-ttu-id="de392-194">在 hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="de392-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![何謂 Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de392-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de392-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="de392-197">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 傳統入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="de392-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="de392-198">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de392-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="de392-199">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="de392-199">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者][100] 

2. <span data-ttu-id="de392-201">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="de392-201">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="de392-202">toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="de392-202">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者][101] 

4. <span data-ttu-id="de392-204">tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="de392-204">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![建立 Azure AD 測試使用者][102] 

5. <span data-ttu-id="de392-206">在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="de392-206">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者][103]
   
    <span data-ttu-id="de392-208">a.</span><span class="sxs-lookup"><span data-stu-id="de392-208">a.</span></span> <span data-ttu-id="de392-209">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="de392-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="de392-210">b.</span><span class="sxs-lookup"><span data-stu-id="de392-210">b.</span></span> <span data-ttu-id="de392-211">在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="de392-211">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="de392-212">c.</span><span class="sxs-lookup"><span data-stu-id="de392-212">c.</span></span> <span data-ttu-id="de392-213">按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="de392-213">Click Next.</span></span>

6. <span data-ttu-id="de392-214">在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="de392-214">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![建立 Azure AD 測試使用者][104] 
   
    <span data-ttu-id="de392-216">a.</span><span class="sxs-lookup"><span data-stu-id="de392-216">a.</span></span> <span data-ttu-id="de392-217">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="de392-217">In hello **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="de392-218">b.</span><span class="sxs-lookup"><span data-stu-id="de392-218">b.</span></span> <span data-ttu-id="de392-219">在 hello**姓氏**文字方塊中，輸入， **Simon**。</span><span class="sxs-lookup"><span data-stu-id="de392-219">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="de392-220">c.</span><span class="sxs-lookup"><span data-stu-id="de392-220">c.</span></span> <span data-ttu-id="de392-221">在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="de392-221">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="de392-222">d.</span><span class="sxs-lookup"><span data-stu-id="de392-222">d.</span></span> <span data-ttu-id="de392-223">在 hello**角色**清單中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="de392-223">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="de392-224">e.</span><span class="sxs-lookup"><span data-stu-id="de392-224">e.</span></span> <span data-ttu-id="de392-225">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="de392-225">Click **Next**.</span></span>

7. <span data-ttu-id="de392-226">在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="de392-226">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者][105]  

8. <span data-ttu-id="de392-228">在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="de392-228">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者][106]   
   
    <span data-ttu-id="de392-230">a.</span><span class="sxs-lookup"><span data-stu-id="de392-230">a.</span></span> <span data-ttu-id="de392-231">請記下 hello hello 值**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="de392-231">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="de392-232">b.</span><span class="sxs-lookup"><span data-stu-id="de392-232">b.</span></span> <span data-ttu-id="de392-233">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="de392-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="de392-234">建立 Questetra BPM Suite 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de392-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="de392-235">hello 本節目標在於 toocreate 呼叫許 Simon Questetra BPM 套件中的使用者。</span><span class="sxs-lookup"><span data-stu-id="de392-235">hello objective of this section is toocreate a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="de392-236">**toocreate 呼叫許 Simon Questetra BPM 套件中的使用者執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de392-236">**toocreate a user called Britta Simon in Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="de392-237">以系統管理員身分登入 tooyour Questetra BPM 套件公司網站。</span><span class="sxs-lookup"><span data-stu-id="de392-237">Sign-on tooyour Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="de392-238">跳過**系統設定 > 使用者清單 > 新的使用者**。</span><span class="sxs-lookup"><span data-stu-id="de392-238">Go too**System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="de392-239">在 hello 新使用者 對話方塊，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="de392-239">On hello New User dialog, perform hello following steps:</span></span> 
   
    ![建立測試使用者][300] 
   
    <span data-ttu-id="de392-241">a.</span><span class="sxs-lookup"><span data-stu-id="de392-241">a.</span></span> <span data-ttu-id="de392-242">在 hello**名稱**文字方塊中，輸入 Azure AD 中的許的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="de392-242">In hello **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="de392-243">b.</span><span class="sxs-lookup"><span data-stu-id="de392-243">b.</span></span> <span data-ttu-id="de392-244">在 hello**電子郵件**文字方塊中，輸入 Azure AD 中的許的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="de392-244">In hello **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="de392-245">c.</span><span class="sxs-lookup"><span data-stu-id="de392-245">c.</span></span> <span data-ttu-id="de392-246">在 hello**密碼**文字方塊中，輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="de392-246">In hello **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="de392-247">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="de392-247">Click **Add new user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="de392-248">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="de392-248">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="de392-249">本節 hello 目標是 tooenabling 許 Simon toouse Azure 單一登入授與他們存取 tooQuestetra BPM 套件。</span><span class="sxs-lookup"><span data-stu-id="de392-249">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooQuestetra BPM Suite.</span></span>

![何謂 Azure AD Connect][200]

<span data-ttu-id="de392-251">**tooassign 許 Simon tooQuestetra BPM 套件時，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de392-251">**tooassign Britta Simon tooQuestetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="de392-252">在 hello Azure 傳統入口網站，tooopen hello 應用程式 檢視，在 hello 目錄檢視中，按一下 **應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="de392-252">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![何謂 Azure AD Connect][201]
2. <span data-ttu-id="de392-254">在 [hello] 應用程式清單中，選取**Questetra BPM 套件**。</span><span class="sxs-lookup"><span data-stu-id="de392-254">In hello applications list, select **Questetra BPM Suite**.</span></span>
   
    ![何謂 Azure AD Connect][205]
3. <span data-ttu-id="de392-256">在 hello 最上層顯示 hello 功能表上，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="de392-256">In hello menu on hello top, click **Users**.</span></span>
   
    ![何謂 Azure AD Connect][202]
4. <span data-ttu-id="de392-258">在 hello 使用者清單中選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="de392-258">In hello Users list, select **Britta Simon**.</span></span>
   
    ![何謂 Azure AD Connect][203]
5. <span data-ttu-id="de392-260">在 hello hello 底部的工具列中按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="de392-260">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![何謂 Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="de392-262">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="de392-262">Testing Single Sign-On</span></span>
<span data-ttu-id="de392-263">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="de392-263">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="de392-264">當您按一下 hello Questetra BPM 套件磚 hello 存取面板中的時，您應該取得自動登入 tooyour Questetra BPM Suite 應用程式。</span><span class="sxs-lookup"><span data-stu-id="de392-264">When you click hello Questetra BPM Suite tile in hello Access Panel, you should get automatically signed-on tooyour Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de392-265">其他資源</span><span class="sxs-lookup"><span data-stu-id="de392-265">Additional Resources</span></span>
* [<span data-ttu-id="de392-266">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de392-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de392-267">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="de392-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
