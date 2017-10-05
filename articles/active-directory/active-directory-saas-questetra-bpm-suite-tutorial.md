---
title: "教學課程：Azure Active Directory 與 Questetra BPM Suite 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Questetra BPM Suite 之間的單一登入。"
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
ms.openlocfilehash: 7ae75446c9d19ce15a82caa9604658a528ab9941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="842b6-103">教學課程：Azure Active Directory 與 Questetra BPM Suite 整合</span><span class="sxs-lookup"><span data-stu-id="842b6-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="842b6-104">本教學課程旨在說明如何整合 Questetra BPM Suite 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="842b6-104">The objective of this tutorial is to show you how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="842b6-105">Questetra BPM Suite 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="842b6-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="842b6-106">您可以在 Azure AD 中控制可存取 Questetra BPM Suite 的人員。</span><span class="sxs-lookup"><span data-stu-id="842b6-106">You can control in Azure AD who has access to Questetra BPM Suite</span></span> 
* <span data-ttu-id="842b6-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Questetra BPM Suite (單一登入)</span><span class="sxs-lookup"><span data-stu-id="842b6-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="842b6-108">您可以在 Azure 傳統入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="842b6-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="842b6-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="842b6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="842b6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="842b6-110">Prerequisites</span></span>
<span data-ttu-id="842b6-111">若要設定 Azure AD 與 Questetra BPM Suite 整合，您需要以下項目：</span><span class="sxs-lookup"><span data-stu-id="842b6-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span></span>

* <span data-ttu-id="842b6-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="842b6-112">An Azure AD subscription</span></span>
* <span data-ttu-id="842b6-113">已啟用 [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="842b6-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="842b6-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="842b6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="842b6-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="842b6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="842b6-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="842b6-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="842b6-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="842b6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="842b6-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="842b6-118">Scenario Description</span></span>
<span data-ttu-id="842b6-119">此教學課程的目標是讓您在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="842b6-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="842b6-120">本教學課程中說明的案例由三個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="842b6-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="842b6-121">從資源庫加入 Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="842b6-121">Adding Questetra BPM Suite from the gallery</span></span> 
2. <span data-ttu-id="842b6-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="842b6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a><span data-ttu-id="842b6-123">從資源庫加入 Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="842b6-123">Adding Questetra BPM Suite from the gallery</span></span>
<span data-ttu-id="842b6-124">若要設定 Questetra BPM Suite 與 Azure AD 整合，您需要從資源庫將 Questetra BPM Suite 加入至受管理 SaaS 應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="842b6-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="842b6-125">**若要從資源庫新增 Questetra BPM Suite，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="842b6-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="842b6-126">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="842b6-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="842b6-128">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="842b6-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="842b6-129">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="842b6-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![應用程式][2]

4. <span data-ttu-id="842b6-131">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="842b6-131">Click **Add** at the bottom of the page.</span></span>
   
    ![應用程式][3]

5. <span data-ttu-id="842b6-133">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="842b6-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![應用程式][4]

6. <span data-ttu-id="842b6-135">在搜尋方塊中，輸入 **Questetra BPM Suite**。</span><span class="sxs-lookup"><span data-stu-id="842b6-135">In the search box, type **Questetra BPM Suite**.</span></span>
   
    ![應用程式][5]

7. <span data-ttu-id="842b6-137">在結果窗格中，選取 [Questetra BPM Suite]，然後按一下 [完成] 以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="842b6-137">In the results pane, select **Questetra BPM Suite**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="842b6-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="842b6-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="842b6-139">本節的目標是說明如何以名為 "Britta Simon" 的測試使用者為基礎，使用 Questetra BPM Suite 來設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="842b6-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="842b6-140">單一登入若要運作，Azure AD 必須知道 Questetra BPM Suite 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="842b6-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite to an user in Azure AD is.</span></span> <span data-ttu-id="842b6-141">換句話說，必須在 Azure AD 使用者和 Questetra BPM Suite 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="842b6-141">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span></span>  
<span data-ttu-id="842b6-142">建立此連結關聯性的方法是將 Azure AD 中的**使用者名稱**的值指定為 Questetra BPM Suite 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="842b6-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="842b6-143">若要使用 Questetra BPM Suite 設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="842b6-143">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="842b6-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="842b6-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="842b6-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="842b6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="842b6-146">**[建立 Questetra BPM Suite 測試使用者](#creating-a-questetra-bpm-suite-test-user)** - 使 Questetra BPM Suite 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="842b6-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="842b6-147">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="842b6-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="842b6-148">**[測試單一登入](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="842b6-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="842b6-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="842b6-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="842b6-150">本節目標是在 Azure 傳統入口網站中啟用 Azure AD 單一登入功能，以及在您的 Questetra BPM Suite 應用程式中設定單一登入功能。</span><span class="sxs-lookup"><span data-stu-id="842b6-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="842b6-151">**若要使用 Questetra BPM Suite 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="842b6-151">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="842b6-152">在 Azure 傳統入口網站的 [Questetra BPM Suite] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="842b6-152">In the Azure classic portal, on the **Questetra BPM Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][8]

2. <span data-ttu-id="842b6-154">在 [要如何讓使用者登入 Questetra BPM Suite] 頁面上，選取 [Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="842b6-154">On the **How would you like users to sign on to Questetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][9]

3. <span data-ttu-id="842b6-156">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 **Questetra BPM Suite** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="842b6-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="842b6-157">在頂端的功能表中，按一下 [系統設定] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-157">In the menu on the top, click **System Settings**.</span></span> 
   
    ![Azure AD 單一登入][10]

5. <span data-ttu-id="842b6-159">若要開啟 [SingleSignOnSAML] 頁面，按一下 [SSO (SAML)]。</span><span class="sxs-lookup"><span data-stu-id="842b6-159">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD 單一登入][11]

6. <span data-ttu-id="842b6-161">在 Azure 傳統入口網站的 [設定應用程式設定]  對話方塊頁面中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="842b6-161">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![設定 App 設定][13]
   
    <span data-ttu-id="842b6-163">a.</span><span class="sxs-lookup"><span data-stu-id="842b6-163">a.</span></span> <span data-ttu-id="842b6-164">在 **Questetra BPM Suite** 公司網站的 [SP 資訊] 區段中，複製 [ACS URL]，然後將它貼入 [登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="842b6-164">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="842b6-165">b.</span><span class="sxs-lookup"><span data-stu-id="842b6-165">b.</span></span> <span data-ttu-id="842b6-166">在 **Questetra BPM Suite** 公司網站的 [SP 資訊] 區段中，複製 [ACS URL]，然後將它貼入 [登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="842b6-166">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **Entity ID**, and then paste it into the **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="842b6-167">c.</span><span class="sxs-lookup"><span data-stu-id="842b6-167">c.</span></span> <span data-ttu-id="842b6-168">在 **Questetra BPM Suite** 公司網站的 [SP 資訊] 區段中，複製 [ACS URL]，然後將它貼入 [回覆 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="842b6-168">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="842b6-169">d.</span><span class="sxs-lookup"><span data-stu-id="842b6-169">d.</span></span> <span data-ttu-id="842b6-170">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-170">Click **Next**.</span></span>

7. <span data-ttu-id="842b6-171">在 [設定在 Questetra BPM Suite 單一登入] 頁面上，按一下 [下載憑證]，然後在本機電腦上儲存憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="842b6-171">On the **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![設定單一登入][14]

8. <span data-ttu-id="842b6-173">在您的 **Questetra BPM Suite** 公司網站上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="842b6-173">On you **Questetra BPM Suite** company site, perform the following steps:</span></span> 
   
    ![設定單一登入][15]
   
    <span data-ttu-id="842b6-175">a.</span><span class="sxs-lookup"><span data-stu-id="842b6-175">a.</span></span> <span data-ttu-id="842b6-176">選取 [啟用單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="842b6-177">b.</span><span class="sxs-lookup"><span data-stu-id="842b6-177">b.</span></span> <span data-ttu-id="842b6-178">在 Azure 傳統入口網站上，複製 [簽發者 URL] 值，然後將它貼到 [實體識別碼] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="842b6-178">On the Azure classic portal, copy the **Issuer URL** value, and then paste it into the **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="842b6-179">c.</span><span class="sxs-lookup"><span data-stu-id="842b6-179">c.</span></span> <span data-ttu-id="842b6-180">在 Azure 傳統入口網站上，複製 [單一登入服務 URL] 值，然後將它貼到 [登入頁面 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="842b6-180">On the Azure classic portal, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="842b6-181">d.</span><span class="sxs-lookup"><span data-stu-id="842b6-181">d.</span></span> <span data-ttu-id="842b6-182">在 Azure 傳統入口網站上，複製 [單一登出服務 URL] 值，然後將它貼到 [登出頁面 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="842b6-182">On the Azure classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="842b6-183">e.</span><span class="sxs-lookup"><span data-stu-id="842b6-183">e.</span></span> <span data-ttu-id="842b6-184">在 [名稱識別碼格式] 文字方塊中，輸入 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**。</span><span class="sxs-lookup"><span data-stu-id="842b6-184">In the **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="842b6-185">f.</span><span class="sxs-lookup"><span data-stu-id="842b6-185">f.</span></span> <span data-ttu-id="842b6-186">從您下載的憑證建立 Base-64 編碼檔案。</span><span class="sxs-lookup"><span data-stu-id="842b6-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="842b6-187">如需詳細資訊，請參閱 [如何將二進位憑證轉換成文字檔](http://youtu.be/PlgrzUZ-Y1o)。</span><span class="sxs-lookup"><span data-stu-id="842b6-187">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="842b6-188">g.</span><span class="sxs-lookup"><span data-stu-id="842b6-188">g.</span></span> <span data-ttu-id="842b6-189">在記事本中開啟 Base-64 編碼的憑證、將其內容複製到剪貼簿，然後將它貼到 [驗證憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="842b6-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="842b6-190">h.</span><span class="sxs-lookup"><span data-stu-id="842b6-190">h.</span></span> <span data-ttu-id="842b6-191">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-191">Click **Save**.</span></span>

1. <span data-ttu-id="842b6-192">在 Azure 傳統入口網站中，選取單一登入設定確認，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-192">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![何謂 Azure AD Connect][17]

2. <span data-ttu-id="842b6-194">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="842b6-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![何謂 Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="842b6-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="842b6-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="842b6-197">本節的目標是要在 Azure 傳統入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="842b6-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="842b6-198">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="842b6-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="842b6-199">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="842b6-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者][100] 

2. <span data-ttu-id="842b6-201">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="842b6-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="842b6-202">若要顯示使用者清單，請按一下頂端功能表中的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-202">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者][101] 

4. <span data-ttu-id="842b6-204">若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="842b6-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![建立 Azure AD 測試使用者][102] 

5. <span data-ttu-id="842b6-206">在 [告訴我們這位使用者]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="842b6-206">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者][103]
   
    <span data-ttu-id="842b6-208">a.</span><span class="sxs-lookup"><span data-stu-id="842b6-208">a.</span></span> <span data-ttu-id="842b6-209">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="842b6-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="842b6-210">b.</span><span class="sxs-lookup"><span data-stu-id="842b6-210">b.</span></span> <span data-ttu-id="842b6-211">在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="842b6-211">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="842b6-212">c.</span><span class="sxs-lookup"><span data-stu-id="842b6-212">c.</span></span> <span data-ttu-id="842b6-213">按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="842b6-213">Click Next.</span></span>

6. <span data-ttu-id="842b6-214">在 [使用者設定檔]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="842b6-214">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![建立 Azure AD 測試使用者][104] 
   
    <span data-ttu-id="842b6-216">a.</span><span class="sxs-lookup"><span data-stu-id="842b6-216">a.</span></span> <span data-ttu-id="842b6-217">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="842b6-217">In the **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="842b6-218">b.</span><span class="sxs-lookup"><span data-stu-id="842b6-218">b.</span></span> <span data-ttu-id="842b6-219">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="842b6-219">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="842b6-220">c.</span><span class="sxs-lookup"><span data-stu-id="842b6-220">c.</span></span> <span data-ttu-id="842b6-221">在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="842b6-221">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="842b6-222">d.</span><span class="sxs-lookup"><span data-stu-id="842b6-222">d.</span></span> <span data-ttu-id="842b6-223">在 [角色] 清單中選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="842b6-223">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="842b6-224">e.</span><span class="sxs-lookup"><span data-stu-id="842b6-224">e.</span></span> <span data-ttu-id="842b6-225">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-225">Click **Next**.</span></span>

7. <span data-ttu-id="842b6-226">在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="842b6-226">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者][105]  

8. <span data-ttu-id="842b6-228">在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="842b6-228">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者][106]   
   
    <span data-ttu-id="842b6-230">a.</span><span class="sxs-lookup"><span data-stu-id="842b6-230">a.</span></span> <span data-ttu-id="842b6-231">記下 [新密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="842b6-231">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="842b6-232">b.</span><span class="sxs-lookup"><span data-stu-id="842b6-232">b.</span></span> <span data-ttu-id="842b6-233">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="842b6-234">建立 Questetra BPM Suite 測試使用者</span><span class="sxs-lookup"><span data-stu-id="842b6-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="842b6-235">本節目標是在 Halogen Software 中建立名為 Questetra BPM Suite 的使用者。</span><span class="sxs-lookup"><span data-stu-id="842b6-235">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="842b6-236">**若要在 Questetra BPM Suite 中建立名為 Britta Simon 的使用者，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="842b6-236">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="842b6-237">以系統管理員身分登入您的 Questetra BPM Suite 公司網站。</span><span class="sxs-lookup"><span data-stu-id="842b6-237">Sign-on to your Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="842b6-238">移至 [系統設定] > [使用者清單] > [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="842b6-238">Go to **System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="842b6-239">在 [新增使用者] 對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="842b6-239">On the New User dialog, perform the following steps:</span></span> 
   
    ![建立測試使用者][300] 
   
    <span data-ttu-id="842b6-241">a.</span><span class="sxs-lookup"><span data-stu-id="842b6-241">a.</span></span> <span data-ttu-id="842b6-242">在 [名稱] 文字方塊中，輸入 Azure AD 中 Britta 的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="842b6-242">In the **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="842b6-243">b.</span><span class="sxs-lookup"><span data-stu-id="842b6-243">b.</span></span> <span data-ttu-id="842b6-244">在 [電子郵件] 文字方塊中，輸入 Azure AD 中 Britta 的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="842b6-244">In the **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="842b6-245">c.</span><span class="sxs-lookup"><span data-stu-id="842b6-245">c.</span></span> <span data-ttu-id="842b6-246">在 [密碼] 文字方塊中輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="842b6-246">In the **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="842b6-247">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-247">Click **Add new user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="842b6-248">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="842b6-248">Assigning the Azure AD test user</span></span>
<span data-ttu-id="842b6-249">本節目標是授與 Britta Simon 對 Questetra BPM Suite 的存取權，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="842b6-249">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Questetra BPM Suite.</span></span>

![何謂 Azure AD Connect][200]

<span data-ttu-id="842b6-251">**若要將 Britta Simon 指派到 Questetra BPM Suite，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="842b6-251">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="842b6-252">在 Azure 傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="842b6-252">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![何謂 Azure AD Connect][201]
2. <span data-ttu-id="842b6-254">在應用程式清單中，選取 [Questetra BPM Suite] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-254">In the applications list, select **Questetra BPM Suite**.</span></span>
   
    ![何謂 Azure AD Connect][205]
3. <span data-ttu-id="842b6-256">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-256">In the menu on the top, click **Users**.</span></span>
   
    ![何謂 Azure AD Connect][202]
4. <span data-ttu-id="842b6-258">在 [使用者] 清單中，選取 [Britta Simon] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-258">In the Users list, select **Britta Simon**.</span></span>
   
    ![何謂 Azure AD Connect][203]
5. <span data-ttu-id="842b6-260">在底部的工具列中，按一下 [指派] 。</span><span class="sxs-lookup"><span data-stu-id="842b6-260">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![何謂 Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="842b6-262">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="842b6-262">Testing Single Sign-On</span></span>
<span data-ttu-id="842b6-263">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="842b6-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="842b6-264">當您在 [存取面板] 中按一下 [Questetra BPM Suite] 磚時，您應該會自動登入您的 Questetra BPM Suite 應用程式。</span><span class="sxs-lookup"><span data-stu-id="842b6-264">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="842b6-265">其他資源</span><span class="sxs-lookup"><span data-stu-id="842b6-265">Additional Resources</span></span>
* [<span data-ttu-id="842b6-266">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="842b6-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="842b6-267">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="842b6-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
