---
title: "教學課程：Azure Active Directory 與 SuccessFactors 整合 | Microsoft Docs"
description: "了解如何使用 SuccessFactors 搭配 Azure Active Directory 來啟用單一登入、自動佈建和更多功能！"
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
ms.openlocfilehash: e85a38ccbe25263ac42bc76351416b023fb77c87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="d1402-103">教學課程：Azure Active Directory 與 SuccessFactors 整合</span><span class="sxs-lookup"><span data-stu-id="d1402-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="d1402-104">本教學課程旨在說明如何整合 SuccessFactors 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d1402-104">The objective of this tutorial is to show you how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1402-105">SuccessFactors 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d1402-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="d1402-106">您可以在 Azure AD 中控制可存取 SuccessFactors 的人員</span><span class="sxs-lookup"><span data-stu-id="d1402-106">You can control in Azure AD who has access to SuccessFactors</span></span>
* <span data-ttu-id="d1402-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SuccessFactors (單一登入)</span><span class="sxs-lookup"><span data-stu-id="d1402-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="d1402-108">您可以在 Azure 傳統入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d1402-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="d1402-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d1402-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1402-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d1402-110">Prerequisites</span></span>
<span data-ttu-id="d1402-111">若要設定 Azure AD 與 SuccessFactors 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d1402-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span></span>

* <span data-ttu-id="d1402-112">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="d1402-112">A valid Azure subscription</span></span>
* <span data-ttu-id="d1402-113">SuccessFactors 中的租用戶</span><span class="sxs-lookup"><span data-stu-id="d1402-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="d1402-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d1402-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="d1402-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d1402-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="d1402-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="d1402-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="d1402-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d1402-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1402-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d1402-118">Scenario description</span></span>
<span data-ttu-id="d1402-119">此教學課程的目標是讓您在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1402-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="d1402-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d1402-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1402-121">從資源庫新增 SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="d1402-121">Adding SuccessFactors from the gallery</span></span>
2. <span data-ttu-id="d1402-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d1402-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-the-gallery"></a><span data-ttu-id="d1402-123">從資源庫新增 SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="d1402-123">Adding SuccessFactors from the gallery</span></span>
<span data-ttu-id="d1402-124">若要設定 SuccessFactors 與 Azure AD 的整合，您需要從資源庫將 SuccessFactors 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="d1402-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d1402-125">**若要從資源庫新增 SuccessFactors，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d1402-125">**To add SuccessFactors from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d1402-126">在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="d1402-126">In the Azure classic portal, on the left navigation panel, click **Active Directory**.</span></span>
   
    ![設定單一登入][1]
2. <span data-ttu-id="d1402-128">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="d1402-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d1402-129">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="d1402-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![設定單一登入][2]
4. <span data-ttu-id="d1402-131">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="d1402-131">Click **Add** at the bottom of the page.</span></span>
   
    ![應用程式][3]
5. <span data-ttu-id="d1402-133">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d1402-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![設定單一登入][4]
6. <span data-ttu-id="d1402-135">在 [搜尋方塊] 中，輸入 **SuccessFactors**。</span><span class="sxs-lookup"><span data-stu-id="d1402-135">In the **search box**, type **SuccessFactors**.</span></span>
   
    ![設定單一登入][5]
7. <span data-ttu-id="d1402-137">在結果窗格中，選取 [SuccessFactors]，然後按一下 [完成] 加入應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1402-137">In the results panel, select **SuccessFactors**, and then click **Complete** to add the application.</span></span>
   
    ![設定單一登入][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d1402-139">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d1402-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d1402-140">本節目標是說明如何以名為 "Britta Simon" 的測試使用者為基礎，使用 SuccessFactors 來設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1402-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d1402-141">若要讓單一登入運作，Azure AD 必須知道 SuccessFactors 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d1402-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors to an user in Azure AD is.</span></span> <span data-ttu-id="d1402-142">換句話說，必須在 Azure AD 使用者和 SuccessFactors 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d1402-142">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span></span>

<span data-ttu-id="d1402-143">建立此連結關聯性的方法是將 Azure AD 中**使用者名稱**的值指派為 SuccessFactors 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="d1402-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SuccessFactors.</span></span>

<span data-ttu-id="d1402-144">若要設定及測試對 SuccessFactors 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d1402-144">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d1402-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d1402-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d1402-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1402-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1402-147">**[建立 SuccessFactors 測試使用者](#creating-a-successfactors-test-user)** - 使 SuccessFactors 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="d1402-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d1402-148">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1402-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d1402-149">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d1402-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d1402-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d1402-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="d1402-151">在本節中，您會在傳統入口網站中啟用 Azure AD 單一登入，並在您的 SuccessFactors 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1402-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="d1402-152">**若要使用 SuccessFactors 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d1402-152">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="d1402-153">在 Azure 傳統入口網站的 [SuccessFactors] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d1402-153">In the Azure classic portal, on the **SuccessFactors** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    ![設定單一登入][7]
2. <span data-ttu-id="d1402-155">在 [要如何讓使用者登入 SuccessFactors] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d1402-155">On the **How would you like users to sign on to SuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![設定單一登入][8]
3. <span data-ttu-id="d1402-157">在 [設定應用程式 URL] 頁面上，執行下列步驟，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d1402-157">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    ![設定單一登入][9]
   
    <span data-ttu-id="d1402-159">a.</span><span class="sxs-lookup"><span data-stu-id="d1402-159">a.</span></span> <span data-ttu-id="d1402-160">在 [登入 URL] 文字方塊中，以下列其中一個模式輸入 URL︰</span><span class="sxs-lookup"><span data-stu-id="d1402-160">In the **Sign On URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="d1402-161">b.</span><span class="sxs-lookup"><span data-stu-id="d1402-161">b.</span></span> <span data-ttu-id="d1402-162">在 [回覆 URL] 文字方塊中，以下列其中一個模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="d1402-162">In the **Reply URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="d1402-163">c.</span><span class="sxs-lookup"><span data-stu-id="d1402-163">c.</span></span> <span data-ttu-id="d1402-164">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d1402-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="d1402-165">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="d1402-165">Please note that these are not the real values.</span></span> <span data-ttu-id="d1402-166">您必須使用實際的「登入 URL」及「回覆 URL」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="d1402-166">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="d1402-167">若要取得這些值，請連絡 [SuccessFactors 支援小組](https://www.successfactors.com/en_us/support.html)。</span><span class="sxs-lookup"><span data-stu-id="d1402-167">To get these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="d1402-168">在 [設定在 SuccessFactors 單一登入] 頁面上，按一下 [下載憑證]，然後在本機電腦上儲存憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="d1402-168">On the **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![設定單一登入][10]

2. <span data-ttu-id="d1402-170">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **SuccessFactors 系統管理入口網站** 。</span><span class="sxs-lookup"><span data-stu-id="d1402-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="d1402-171">造訪 [應用程式安全性] 和原生 [單一登入功能]。</span><span class="sxs-lookup"><span data-stu-id="d1402-171">Visit **Application Security** and native to **Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="d1402-172">在 [重設權杖] 中放入任何值，然後按一下 [儲存權杖] 以啟用 SAML SSO。</span><span class="sxs-lookup"><span data-stu-id="d1402-172">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span></span>
   
    ![在應用程式端設定單一登入][11]

    > [!NOTE] 
    > <span data-ttu-id="d1402-174">此值只是做為 on/off 開關。</span><span class="sxs-lookup"><span data-stu-id="d1402-174">This value is just used as the on/off switch.</span></span> <span data-ttu-id="d1402-175">如果儲存了任何值，SAML SSO 為 ON。</span><span class="sxs-lookup"><span data-stu-id="d1402-175">If any value is saved, the SAML SSO is ON.</span></span> <span data-ttu-id="d1402-176">如果儲存了空白值，SAML SSO 為 OFF。</span><span class="sxs-lookup"><span data-stu-id="d1402-176">If a blank value is saved the SAML SSO is OFF.</span></span>

1. <span data-ttu-id="d1402-177">原生以下螢幕擷取畫面，並執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="d1402-177">Native to below screenshot and perform the following actions.</span></span>
   
    ![在應用程式端設定單一登入][12]
   
    <span data-ttu-id="d1402-179">a.</span><span class="sxs-lookup"><span data-stu-id="d1402-179">a.</span></span> <span data-ttu-id="d1402-180">選取 [SAML v2 SSO] 選項按鈕</span><span class="sxs-lookup"><span data-stu-id="d1402-180">Select the **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="d1402-181">b.</span><span class="sxs-lookup"><span data-stu-id="d1402-181">b.</span></span> <span data-ttu-id="d1402-182">設定 SAML 判斷提示方名稱 (例如 SAML 簽發者 + 公司名稱)。</span><span class="sxs-lookup"><span data-stu-id="d1402-182">Set the SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="d1402-183">c.</span><span class="sxs-lookup"><span data-stu-id="d1402-183">c.</span></span> <span data-ttu-id="d1402-184">在 [SAML 簽發者] 文字方塊中，放入得自 Azure AD 應用程式組態精靈的 [簽發者 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="d1402-184">In the **SAML Issuer** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="d1402-185">d.</span><span class="sxs-lookup"><span data-stu-id="d1402-185">d.</span></span> <span data-ttu-id="d1402-186">選取 [回應 (客戶產生的/IdP/AP)] 做為 [需要必要簽章]。</span><span class="sxs-lookup"><span data-stu-id="d1402-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="d1402-187">e.</span><span class="sxs-lookup"><span data-stu-id="d1402-187">e.</span></span> <span data-ttu-id="d1402-188">選取 [啟用] 做為 [啟用 SAML 旗標]。</span><span class="sxs-lookup"><span data-stu-id="d1402-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="d1402-189">f.</span><span class="sxs-lookup"><span data-stu-id="d1402-189">f.</span></span> <span data-ttu-id="d1402-190">選取 [否] 做為 [登入要求簽章 (SF 產生的/SP/RP)]。</span><span class="sxs-lookup"><span data-stu-id="d1402-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="d1402-191">g.</span><span class="sxs-lookup"><span data-stu-id="d1402-191">g.</span></span> <span data-ttu-id="d1402-192">選取 [瀏覽器/後置設定檔] 做為 [SAML 設定檔]。</span><span class="sxs-lookup"><span data-stu-id="d1402-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="d1402-193">h.</span><span class="sxs-lookup"><span data-stu-id="d1402-193">h.</span></span> <span data-ttu-id="d1402-194">選取 [否] 做為 [強制執行憑證有效期間]。</span><span class="sxs-lookup"><span data-stu-id="d1402-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="d1402-195">i.</span><span class="sxs-lookup"><span data-stu-id="d1402-195">i.</span></span> <span data-ttu-id="d1402-196">複製所下載憑證檔案的內容，然後將它貼至 [SAML 驗證憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="d1402-196">Copy the content of the downloaded certificate file, and then paste it into the **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d1402-197">憑證內容必須有開始憑證和結束憑證標籤。</span><span class="sxs-lookup"><span data-stu-id="d1402-197">The certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="d1402-198">瀏覽至 [SAML V2]，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1402-198">Navigate to SAML V2, and then perform the following steps:</span></span>
   
    ![在應用程式端設定單一登入][13]
   
    <span data-ttu-id="d1402-200">a.</span><span class="sxs-lookup"><span data-stu-id="d1402-200">a.</span></span> <span data-ttu-id="d1402-201">選取 [是] 做為 [支援 SP 起始的全域登出]。</span><span class="sxs-lookup"><span data-stu-id="d1402-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="d1402-202">b.</span><span class="sxs-lookup"><span data-stu-id="d1402-202">b.</span></span> <span data-ttu-id="d1402-203">在 [全域登出服務 URL (LogoutRequest 目的地)] 文字方塊中，放入得自 Azure AD 應用程式組態精靈的 [遠端登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="d1402-203">In the **Global Logout Service URL (LogoutRequest destination)** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="d1402-204">c.</span><span class="sxs-lookup"><span data-stu-id="d1402-204">c.</span></span> <span data-ttu-id="d1402-205">選取 [否] 做為 [要求 SP 必須加密所有 NameID 元素]。</span><span class="sxs-lookup"><span data-stu-id="d1402-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="d1402-206">d.</span><span class="sxs-lookup"><span data-stu-id="d1402-206">d.</span></span> <span data-ttu-id="d1402-207">選取 [未指定] 做為 [NameID 格式]。</span><span class="sxs-lookup"><span data-stu-id="d1402-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="d1402-208">e.</span><span class="sxs-lookup"><span data-stu-id="d1402-208">e.</span></span> <span data-ttu-id="d1402-209">選取 [是] 做為 [啟用 SP 起始的登入 (AuthnRequest)]。</span><span class="sxs-lookup"><span data-stu-id="d1402-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="d1402-210">f.</span><span class="sxs-lookup"><span data-stu-id="d1402-210">f.</span></span> <span data-ttu-id="d1402-211">在 [以全公司簽發者身分傳送要求] 文字方塊中，放入得自 Azure AD 應用程式組態精靈的 [遠端登入 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="d1402-211">In the **Send request as Company-Wide issuer** textbox put the value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="d1402-212">如果您想要讓登入使用者名稱不區分大小寫，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="d1402-212">Perform these steps if you want to make the login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="d1402-213">a.</span><span class="sxs-lookup"><span data-stu-id="d1402-213">a.</span></span> <span data-ttu-id="d1402-214">造訪 [公司設定] \(靠近底部)。</span><span class="sxs-lookup"><span data-stu-id="d1402-214">Visit **Company Settings**(near the bottom).</span></span>
   
    <span data-ttu-id="d1402-215">b.</span><span class="sxs-lookup"><span data-stu-id="d1402-215">b.</span></span> <span data-ttu-id="d1402-216">選取 [啟用不區分大小寫使用者名稱] 附近的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d1402-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="d1402-217">c. 按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d1402-217">c.Click **Save**.</span></span>
   
    ![設定單一登入][29]

    > [!NOTE] 
    > <span data-ttu-id="d1402-219">如果您嘗試啟用此功能，系統會檢查它是否會建立重複的 SAML 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="d1402-219">If you try to enable this, the system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="d1402-220">例如，如果客戶有 User1 和 user1 的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d1402-220">For example if the customer has usernames User1 and user1.</span></span> <span data-ttu-id="d1402-221">取消區分大小寫功能將會讓這些名稱重複。</span><span class="sxs-lookup"><span data-stu-id="d1402-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="d1402-222">系統會提供您錯誤訊息，並將不會啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="d1402-222">The system will give you an error message and will not enable the feature.</span></span> <span data-ttu-id="d1402-223">客戶需要變更其中一個使用者名稱，使其拼寫方式實際上不同。</span><span class="sxs-lookup"><span data-stu-id="d1402-223">The customer will need to change one of the usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="d1402-224">在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d1402-224">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    ![應用程式][14]
2. <span data-ttu-id="d1402-226">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="d1402-226">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![應用程式][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d1402-228">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d1402-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="d1402-229">本節的目標是要在傳統入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d1402-229">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][16]

<span data-ttu-id="d1402-231">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d1402-231">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d1402-232">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="d1402-232">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者][17]
2. <span data-ttu-id="d1402-234">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="d1402-234">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d1402-235">若要顯示使用者清單，請按一下頂端功能表的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="d1402-235">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者][18]
4. <span data-ttu-id="d1402-237">若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="d1402-237">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![建立 Azure AD 測試使用者][19]
5. <span data-ttu-id="d1402-239">在 [告訴我們這位使用者]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1402-239">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者][20]
   
    <span data-ttu-id="d1402-241">a.</span><span class="sxs-lookup"><span data-stu-id="d1402-241">a.</span></span> <span data-ttu-id="d1402-242">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="d1402-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="d1402-243">b.</span><span class="sxs-lookup"><span data-stu-id="d1402-243">b.</span></span> <span data-ttu-id="d1402-244">在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d1402-244">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="d1402-245">c.</span><span class="sxs-lookup"><span data-stu-id="d1402-245">c.</span></span> <span data-ttu-id="d1402-246">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d1402-246">Click **Next**.</span></span>
6. <span data-ttu-id="d1402-247">在 [使用者設定檔]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1402-247">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者][21]
   
    <span data-ttu-id="d1402-249">a.</span><span class="sxs-lookup"><span data-stu-id="d1402-249">a.</span></span> <span data-ttu-id="d1402-250">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="d1402-250">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="d1402-251">b.</span><span class="sxs-lookup"><span data-stu-id="d1402-251">b.</span></span> <span data-ttu-id="d1402-252">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="d1402-252">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="d1402-253">c.</span><span class="sxs-lookup"><span data-stu-id="d1402-253">c.</span></span> <span data-ttu-id="d1402-254">在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="d1402-254">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="d1402-255">d.</span><span class="sxs-lookup"><span data-stu-id="d1402-255">d.</span></span> <span data-ttu-id="d1402-256">在 [角色] 清單中選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="d1402-256">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="d1402-257">e.</span><span class="sxs-lookup"><span data-stu-id="d1402-257">e.</span></span> <span data-ttu-id="d1402-258">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d1402-258">Click **Next**.</span></span>
7. <span data-ttu-id="d1402-259">在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="d1402-259">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者][22]
8. <span data-ttu-id="d1402-261">在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1402-261">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者][23]
   
    <span data-ttu-id="d1402-263">a.</span><span class="sxs-lookup"><span data-stu-id="d1402-263">a.</span></span> <span data-ttu-id="d1402-264">記下 [新密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d1402-264">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="d1402-265">b.</span><span class="sxs-lookup"><span data-stu-id="d1402-265">b.</span></span> <span data-ttu-id="d1402-266">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="d1402-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="d1402-267">建立 SuccessFactors 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d1402-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="d1402-268">若要讓 Azure AD 使用者能夠登入 SuccessFactors，必須將他們佈建到 SuccessFactors。</span><span class="sxs-lookup"><span data-stu-id="d1402-268">In order to enable Azure AD users to log into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="d1402-269">SuccessFactors 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="d1402-269">In the case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="d1402-270">若要在 SuccessFactors 建立使用者，您需要連絡 [SuccessFactors 支援小組](https://www.successfactors.com/en_us/support.html)。</span><span class="sxs-lookup"><span data-stu-id="d1402-270">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d1402-271">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d1402-271">Assigning the Azure AD test user</span></span>
<span data-ttu-id="d1402-272">本節的目標是授與 Britta Simon 對 SuccessFactors 的存取權，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1402-272">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SuccessFactors.</span></span>

![指派使用者][24]

<span data-ttu-id="d1402-274">**若要將 Britta Simon 指派到 SuccessFactors，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d1402-274">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="d1402-275">在傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="d1402-275">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![指派使用者][25]
2. <span data-ttu-id="d1402-277">在應用程式清單中，選取 [SuccessFactors] 。</span><span class="sxs-lookup"><span data-stu-id="d1402-277">In the applications list, select **SuccessFactors**.</span></span>
   
    ![設定單一登入][26]
3. <span data-ttu-id="d1402-279">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="d1402-279">In the menu on the top, click **Users**.</span></span>
   
    ![指派使用者][27]
4. <span data-ttu-id="d1402-281">在 [使用者] 清單中，選取 [Britta Simon] 。</span><span class="sxs-lookup"><span data-stu-id="d1402-281">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="d1402-282">在底部的工具列中，按一下 [指派] 。</span><span class="sxs-lookup"><span data-stu-id="d1402-282">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![指派使用者][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="d1402-284">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d1402-284">Testing single sign-on</span></span>
<span data-ttu-id="d1402-285">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="d1402-285">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d1402-286">當您在存取面板中按一下 [SuccessFactors] 圖格時，應該會自動登入您的 SuccessFactors 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1402-286">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1402-287">其他資源</span><span class="sxs-lookup"><span data-stu-id="d1402-287">Additional resources</span></span>
* [<span data-ttu-id="d1402-288">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d1402-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1402-289">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d1402-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
