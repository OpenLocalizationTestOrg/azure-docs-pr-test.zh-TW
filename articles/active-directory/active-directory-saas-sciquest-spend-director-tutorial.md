---
title: "教學課程：Azure Active Directory 與 SciQuest Spend Director 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SciQuest 花主管之間。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="bba7f-103">教學課程：Azure Active Directory 與 SciQuest Spend Director 整合</span><span class="sxs-lookup"><span data-stu-id="bba7f-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="bba7f-104">本教學課程的 hello 目標是 tooshow 您如何 toointegrate SciQuest 花導向器搭配 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="bba7f-104">hello objective of this tutorial is tooshow you how toointegrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="bba7f-105">與 Azure AD 整合 SciQuest 花主管可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="bba7f-105">Integrating SciQuest Spend Director with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="bba7f-106">您可以在 Azure AD 中已存取 tooSciQuest 支出主管人員控制</span><span class="sxs-lookup"><span data-stu-id="bba7f-106">You can control in Azure AD who has access tooSciQuest Spend Director</span></span> 
* <span data-ttu-id="bba7f-107">您可以啟用您的使用者 tooautomatically get 登入 tooSciQuest （單一登入） 具有其 Azure AD 帳戶的支出導向器</span><span class="sxs-lookup"><span data-stu-id="bba7f-107">You can enable your users tooautomatically get signed-on tooSciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="bba7f-108">您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="bba7f-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="bba7f-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="bba7f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bba7f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="bba7f-110">Prerequisites</span></span>
<span data-ttu-id="bba7f-111">tooconfigure SciQuest 花導向器與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="bba7f-111">tooconfigure Azure AD integration with SciQuest Spend Director, you need hello following items:</span></span>

* <span data-ttu-id="bba7f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bba7f-112">An Azure AD subscription</span></span>
* <span data-ttu-id="bba7f-113">啟用 SciQuest Spend Director 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bba7f-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bba7f-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="bba7f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="bba7f-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="bba7f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="bba7f-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="bba7f-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="bba7f-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="bba7f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="bba7f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="bba7f-118">Scenario Description</span></span>
<span data-ttu-id="bba7f-119">本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 單一登入的測試環境中。</span><span class="sxs-lookup"><span data-stu-id="bba7f-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="bba7f-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="bba7f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bba7f-121">從 hello 圖庫加入 SciQuest 花導向器</span><span class="sxs-lookup"><span data-stu-id="bba7f-121">Adding SciQuest Spend Director from hello gallery</span></span> 
2. <span data-ttu-id="bba7f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bba7f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a><span data-ttu-id="bba7f-123">從 hello 圖庫加入 SciQuest 花導向器</span><span class="sxs-lookup"><span data-stu-id="bba7f-123">Adding SciQuest Spend Director from hello gallery</span></span>
<span data-ttu-id="bba7f-124">tooconfigure hello 整合 SciQuest 花主管到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SciQuest 花導向器。</span><span class="sxs-lookup"><span data-stu-id="bba7f-124">tooconfigure hello integration of SciQuest Spend Director into Azure AD, you need tooadd SciQuest Spend Director from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bba7f-125">**tooadd SciQuest 花導演 hello 圖庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bba7f-125">**tooadd SciQuest Spend Director from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bba7f-126">在 [hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="bba7f-128">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="bba7f-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="bba7f-129">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="bba7f-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![應用程式][2]

4. <span data-ttu-id="bba7f-131">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="bba7f-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![應用程式][3]

5. <span data-ttu-id="bba7f-133">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![應用程式][4]

6. <span data-ttu-id="bba7f-135">在 [hello] 搜尋方塊中，輸入**sciQuest 花主管**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-135">In hello search box, type **sciQuest spend director**.</span></span>
   
    ![應用程式][5]

7. <span data-ttu-id="bba7f-137">在 [hello] 結果窗格中，選取**SciQuest 花主管**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bba7f-137">In hello results pane, select **SciQuest Spend Director**, and then click **Complete** tooadd hello application.</span></span>
   
    ![應用程式][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bba7f-139">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bba7f-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bba7f-140">hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD 單一登入與 SciQuest 花導向器根據稱為 「 許 Simon"的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="bba7f-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bba7f-141">單一登入 toowork，Azure AD 需要 tooknow SciQuest 花主管 tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="bba7f-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SciQuest Spend Director tooan user in Azure AD is.</span></span> <span data-ttu-id="bba7f-142">換句話說，Azure AD 使用者與 hello SciQuest 花導向器中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="bba7f-142">In other words, a link relationship between an Azure AD user and hello related user in SciQuest Spend Director needs toobe established.</span></span>  
<span data-ttu-id="bba7f-143">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**SciQuest 花導向器中。</span><span class="sxs-lookup"><span data-stu-id="bba7f-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="bba7f-144">tooconfigure 及測試 Azure AD 單一登入與 SciQuest 花導向器，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="bba7f-144">tooconfigure and test Azure AD single sign-on with SciQuest Spend Director, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bba7f-145">**[設定 Azure AD 單一單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="bba7f-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bba7f-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="bba7f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bba7f-147">**[建立測試使用者 SciQuest 花主管](#creating-a-halogen-software-test-user)** -toohave 許 Simon SciQuest 花導向器所連結的 toohello Azure AD 的她的表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="bba7f-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in SciQuest Spend Director that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="bba7f-148">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bba7f-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bba7f-149">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="bba7f-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="bba7f-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bba7f-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="bba7f-151">本節 hello 目標是 tooenable Azure AD 單一登入 Azure 傳統入口網站 hello 和 tooconfigure 單一登入 SciQuest 花導向器應用程式中。</span><span class="sxs-lookup"><span data-stu-id="bba7f-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="bba7f-152">**Azure AD 單一登入的 tooconfigure SciQuest 花導向器，以執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="bba7f-152">**tooconfigure Azure AD single sign-on with SciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="bba7f-153">在 Azure 傳統入口網站，在 [hello hello **SciQuest 花主管**應用程式整合頁面上，按一下 [**設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bba7f-153">In hello Azure classic portal, on hello **SciQuest Spend Director** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][8]

2. <span data-ttu-id="bba7f-155">Hello 上**如何想您 tooSciQuest 支出導向器上的使用者 toosign**頁面上，選取**Azure AD 單一登入**，然後按一下 [**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-155">On hello **How would you like users toosign on tooSciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][9]

3. <span data-ttu-id="bba7f-157">在 [hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bba7f-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![設定 App 設定][10]
   
     <span data-ttu-id="bba7f-159">a.</span><span class="sxs-lookup"><span data-stu-id="bba7f-159">a.</span></span> <span data-ttu-id="bba7f-160">在 [hello**登入 URL**文字方塊中，輸入您的使用者 toosign 上使用下列模式的 hello tooyour SciQuest 花導向器應用程式所使用的 URL: *https://。*sciquest.com/.**</span><span class="sxs-lookup"><span data-stu-id="bba7f-160">In hello **Sign On URL** textbox, type your URL used by your users toosign on tooyour SciQuest Spend Director application using hello following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="bba7f-161">b.</span><span class="sxs-lookup"><span data-stu-id="bba7f-161">b.</span></span> <span data-ttu-id="bba7f-162">在 [hello**回覆 URL**文字方塊中，型別 hello 相同值已輸入 hello**登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="bba7f-162">In hello **Reply URL** textbox, type hello same value you have typed into hello **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="bba7f-163">c.</span><span class="sxs-lookup"><span data-stu-id="bba7f-163">c.</span></span> <span data-ttu-id="bba7f-164">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bba7f-164">Click **Next**.</span></span>

4. <span data-ttu-id="bba7f-165">在 [hello **SciQuest 花主管在設定單一登入**頁面上，按一下**下載中繼資料**，然後儲存在本機電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="bba7f-165">On hello **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
    ![何謂 Azure AD Connect][11]

5. <span data-ttu-id="bba7f-167">請連絡 SciQuest 支援 tooenable 這種驗證方法使用 hello 上述下載中繼資料。</span><span class="sxs-lookup"><span data-stu-id="bba7f-167">Contact SciQuest support tooenable this authentication method using hello above downloaded metadata.</span></span>

6. <span data-ttu-id="bba7f-168">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bba7f-168">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span> 
   
    ![何謂 Azure AD Connect][15]

7. <span data-ttu-id="bba7f-170">在 [hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-170">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bba7f-171">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bba7f-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="bba7f-172">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 傳統入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="bba7f-172">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="bba7f-173">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bba7f-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bba7f-174">在 [hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-174">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![何謂 Azure AD Connect][100] 

2. <span data-ttu-id="bba7f-176">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="bba7f-176">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="bba7f-177">toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-177">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![何謂 Azure AD Connect][101] 

4. <span data-ttu-id="bba7f-179">tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-179">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![何謂 Azure AD Connect][102] 

5. <span data-ttu-id="bba7f-181">在 [hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bba7f-181">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![何謂 Azure AD Connect][103] 
   
    <span data-ttu-id="bba7f-183">a.</span><span class="sxs-lookup"><span data-stu-id="bba7f-183">a.</span></span> <span data-ttu-id="bba7f-184">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="bba7f-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="bba7f-185">b.</span><span class="sxs-lookup"><span data-stu-id="bba7f-185">b.</span></span> <span data-ttu-id="bba7f-186">在 [hello 使用者名稱**文字方塊**，型別**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="bba7f-187">c.</span><span class="sxs-lookup"><span data-stu-id="bba7f-187">c.</span></span> <span data-ttu-id="bba7f-188">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bba7f-188">Click **Next**.</span></span>

6. <span data-ttu-id="bba7f-189">在 [hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bba7f-189">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![何謂 Azure AD Connect][104] 
   
    <span data-ttu-id="bba7f-191">a.</span><span class="sxs-lookup"><span data-stu-id="bba7f-191">a.</span></span> <span data-ttu-id="bba7f-192">在 [hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-192">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="bba7f-193">b.</span><span class="sxs-lookup"><span data-stu-id="bba7f-193">b.</span></span> <span data-ttu-id="bba7f-194">在 [hello**姓氏**txtbox，型別， **Simon**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-194">In hello **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="bba7f-195">c.</span><span class="sxs-lookup"><span data-stu-id="bba7f-195">c.</span></span> <span data-ttu-id="bba7f-196">在 [hello**顯示名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-196">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="bba7f-197">d.</span><span class="sxs-lookup"><span data-stu-id="bba7f-197">d.</span></span> <span data-ttu-id="bba7f-198">在 [hello**角色**清單中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-198">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="bba7f-199">e.</span><span class="sxs-lookup"><span data-stu-id="bba7f-199">e.</span></span> <span data-ttu-id="bba7f-200">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bba7f-200">Click **Next**.</span></span>

7. <span data-ttu-id="bba7f-201">在 [hello**取得暫時密碼**對話方塊頁面上，按一下 [**建立**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-201">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![何謂 Azure AD Connect][105]  

8. <span data-ttu-id="bba7f-203">在 [hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bba7f-203">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![何謂 Azure AD Connect][106]   
   
    <span data-ttu-id="bba7f-205">a.</span><span class="sxs-lookup"><span data-stu-id="bba7f-205">a.</span></span> <span data-ttu-id="bba7f-206">請記下 hello hello 值**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-206">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="bba7f-207">b.</span><span class="sxs-lookup"><span data-stu-id="bba7f-207">b.</span></span> <span data-ttu-id="bba7f-208">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="bba7f-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="bba7f-209">建立 SciQuest Spend Director 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bba7f-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="bba7f-210">hello 本節目標在於 toocreate 呼叫許 Simon SciQuest 花導向器中的使用者。</span><span class="sxs-lookup"><span data-stu-id="bba7f-210">hello objective of this section is toocreate a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="bba7f-211">您需要 toocontact SciQuest 花主管支援小組，並為他們提供有關您建立它的測試帳戶 tooget hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bba7f-211">You need toocontact your SciQuest Spend Director support team and provide them with hello details about your test account tooget it created.</span></span>

<span data-ttu-id="bba7f-212">您也可以利用 Just-In-Time 佈建功能，這是 SciQuest Spend Director 支援的單一登入功能。</span><span class="sxs-lookup"><span data-stu-id="bba7f-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="bba7f-213">啟用 Just-In-Time 佈建時，如果使用者不存在，SciQuest Spend Director 就會在使用者嘗試執行單一登入期間自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="bba7f-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="bba7f-214">這項功能會排除 hello 需要 toomanually 建立單一登入對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="bba7f-214">This feature eliminates hello need toomanually create single sign-on counterpart users.</span></span>

<span data-ttu-id="bba7f-215">tooget 中 just-in-time 佈建啟用，您需要 toocontact 正在 SciQuest 花主管支援小組。</span><span class="sxs-lookup"><span data-stu-id="bba7f-215">tooget just-in-time provisioning enabled, you need toocontact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bba7f-216">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="bba7f-216">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="bba7f-217">本節 hello 目標是 tooenabling 許 Simon toouse Azure 單一登入授與他們存取 tooSciQuest 支出導向器。</span><span class="sxs-lookup"><span data-stu-id="bba7f-217">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSciQuest Spend Director.</span></span>

![何謂 Azure AD Connect][200]

<span data-ttu-id="bba7f-219">**tooassign 許 Simon tooSciQuest 支出導向器，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bba7f-219">**tooassign Britta Simon tooSciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="bba7f-220">在 [hello Azure 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="bba7f-220">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![何謂 Azure AD Connect][201]

2. <span data-ttu-id="bba7f-222">在 [hello] 應用程式清單中，選取**SciQuest 花主管**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-222">In hello applications list, select **SciQuest Spend Director**.</span></span>
   
    ![何謂 Azure AD Connect][202]

3. <span data-ttu-id="bba7f-224">在 [hello 最上層顯示 hello 功能表上，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-224">In hello menu on hello top, click **Users**.</span></span>
   
    ![何謂 Azure AD Connect][203]

4. <span data-ttu-id="bba7f-226">在 hello 使用者清單中選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-226">In hello Users list, select **Britta Simon**.</span></span>
   
    ![何謂 Azure AD Connect][204]

5. <span data-ttu-id="bba7f-228">在 hello hello 底部的工具列中按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="bba7f-228">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![何謂 Azure AD Connect][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="bba7f-230">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="bba7f-230">Testing Single Sign-On</span></span>
<span data-ttu-id="bba7f-231">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="bba7f-231">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="bba7f-232">當您按一下 hello SciQuest 花主管磚 hello 存取面板中的時，您應該取得自動登入 tooyour SciQuest 花導向器應用程式。</span><span class="sxs-lookup"><span data-stu-id="bba7f-232">When you click hello SciQuest Spend Director tile in hello Access Panel, you should get automatically signed-on tooyour SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bba7f-233">其他資源</span><span class="sxs-lookup"><span data-stu-id="bba7f-233">Additional Resources</span></span>
* [<span data-ttu-id="bba7f-234">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bba7f-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bba7f-235">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="bba7f-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

