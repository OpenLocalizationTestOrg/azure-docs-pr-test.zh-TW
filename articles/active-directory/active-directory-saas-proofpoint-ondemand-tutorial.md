---
title: "教學課程：Azure Active Directory 與 Proofpoint on Demand 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Proofpoint on Demand 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: b4c8d8c187fc865a905016f04a41843894249f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="10307-103">教學課程：Azure Active Directory 與 Proofpoint on Demand 整合</span><span class="sxs-lookup"><span data-stu-id="10307-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="10307-104">在本教學課程中，您會了解如何整合 Proofpoint on Demand 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="10307-104">In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="10307-105">Proofpoint on Demand 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="10307-105">Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="10307-106">您可以在 Azure AD 中控制可存取 Proofpoint on Demand 的人員</span><span class="sxs-lookup"><span data-stu-id="10307-106">You can control in Azure AD who has access to Proofpoint on Demand</span></span>
- <span data-ttu-id="10307-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Proofpoint on Demand (單一登入)</span><span class="sxs-lookup"><span data-stu-id="10307-107">You can enable your users to automatically get signed-on to Proofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="10307-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="10307-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="10307-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="10307-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10307-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="10307-110">Prerequisites</span></span>

<span data-ttu-id="10307-111">若要設定 Azure AD 與 Proofpoint on Demand 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="10307-111">To configure Azure AD integration with Proofpoint on Demand, you need the following items:</span></span>

- <span data-ttu-id="10307-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="10307-112">An Azure AD subscription</span></span>
- <span data-ttu-id="10307-113">啟用 Proofpoint on Demand 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="10307-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="10307-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="10307-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="10307-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="10307-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="10307-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="10307-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="10307-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="10307-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="10307-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="10307-118">Scenario description</span></span>
<span data-ttu-id="10307-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="10307-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="10307-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="10307-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="10307-121">從資源庫新增 Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="10307-121">Adding Proofpoint on Demand from the gallery</span></span>
2. <span data-ttu-id="10307-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="10307-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-the-gallery"></a><span data-ttu-id="10307-123">從資源庫新增 Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="10307-123">Adding Proofpoint on Demand from the gallery</span></span>
<span data-ttu-id="10307-124">若要設定將 Proofpoint on Demand 整合到 Azure AD 中，您需要從資源庫將 Proofpoint on Demand 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="10307-124">To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="10307-125">**若要從資源庫新增 Proofpoint on Demand，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="10307-125">**To add Proofpoint on Demand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="10307-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="10307-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="10307-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="10307-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="10307-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="10307-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="10307-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="10307-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="10307-133">在搜尋方塊中，輸入 **Proofpoint on Demand**。</span><span class="sxs-lookup"><span data-stu-id="10307-133">In the search box, type **Proofpoint on Demand**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="10307-135">在結果窗格中，選取 [Proofpoint on Demand]，然後按一下 [新增] 按鈕，以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="10307-135">In the results panel, select **Proofpoint on Demand**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="10307-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="10307-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="10307-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Proofpoint on Demand 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="10307-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="10307-139">若要讓單一登入能夠運作，Azure AD 必須知道 Proofpoint on Demand 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="10307-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD.</span></span> <span data-ttu-id="10307-140">換句話說，您必須建立 Azure AD 使用者和 Proofpoint on Demand 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="10307-140">In other words, a link relationship between an Azure AD user and the related user in Proofpoint on Demand needs to be established.</span></span>

<span data-ttu-id="10307-141">建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值指派為 Proofpoint on Demand 中 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="10307-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="10307-142">若要設定及測試與 Proofpoint on Demand 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="10307-142">To configure and test Azure AD single sign-on with Proofpoint on Demand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="10307-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="10307-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="10307-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="10307-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="10307-145">**[建立 Proofpoint 測試使用者](#creating-a-proofpoint-on-demand-test-user)** - 使 Proofpoint 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="10307-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="10307-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="10307-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="10307-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="10307-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="10307-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="10307-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="10307-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Proofpoint on Demand 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="10307-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="10307-150">**若要使用 Proofpoint on Demand 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="10307-150">**To configure Azure AD single sign-on with Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="10307-151">在 Azure 入口網站的 [Proofpoint on Demand] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="10307-151">In the Azure portal, on the **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="10307-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="10307-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
  
    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="10307-155">在 [Proofpoint on Demand 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="10307-155">On the **Proofpoint on Demand Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="10307-157">a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="10307-157">a.In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="10307-158">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="10307-158">b.</span></span> <span data-ttu-id="10307-159">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="10307-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="10307-160">c.</span><span class="sxs-lookup"><span data-stu-id="10307-160">c.</span></span>  <span data-ttu-id="10307-161">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="10307-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="10307-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="10307-162">These values are not the real.</span></span> <span data-ttu-id="10307-163">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="10307-163">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="10307-164">請連絡 [Proofpoint on Demand 用戶端支援小組](https://www.proofpoint.com/us/support-services)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="10307-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to get these values.</span></span> 

4. <span data-ttu-id="10307-165">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="10307-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="10307-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="10307-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="10307-169">在 [Proofpoint on Demand 組態] 區段中，按一下 [設定 Proofpoint on Demand]，以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="10307-169">On the **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="10307-170">從 [快速參考] 區段中複製 **SAML 實體識別碼和 SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="10307-170">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="10307-172">若要在 **Proofpoint on Demand** 端設定單一登入，您必須將已下載的**憑證 (Base64)**、**SAML 實體識別碼**及 **SAML 單一登入服務 URL** 傳送給 [Proofpoint on Demand 用戶端支援小組](https://www.proofpoint.com/us/support-services)。</span><span class="sxs-lookup"><span data-stu-id="10307-172">To configure single sign-on on **Proofpoint on Demand** side, you need to send the downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="10307-173">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="10307-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="10307-174">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="10307-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="10307-175">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="10307-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="10307-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="10307-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="10307-177">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="10307-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="10307-179">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="10307-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="10307-180">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="10307-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="10307-182">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="10307-182">These values are not the real.</span></span> <span data-ttu-id="10307-183">使用實際值來更新這些值</span><span class="sxs-lookup"><span data-stu-id="10307-183">Update these values with the actual</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="10307-185">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="10307-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="10307-187">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="10307-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="10307-189">a.</span><span class="sxs-lookup"><span data-stu-id="10307-189">a.</span></span> <span data-ttu-id="10307-190">在 [名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="10307-190">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="10307-191">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="10307-191">b.</span></span> <span data-ttu-id="10307-192">在 [使用者名稱] 文字方塊中，輸入 Britta Simon 的「電子郵件地址」。</span><span class="sxs-lookup"><span data-stu-id="10307-192">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="10307-193">c.</span><span class="sxs-lookup"><span data-stu-id="10307-193">c.</span></span> <span data-ttu-id="10307-194">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="10307-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="10307-195">d.</span><span class="sxs-lookup"><span data-stu-id="10307-195">d.</span></span> <span data-ttu-id="10307-196">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="10307-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="10307-197">建立 Proofpoint on Demand 測試使用者</span><span class="sxs-lookup"><span data-stu-id="10307-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="10307-198">在本節中，您會在 Proofpoint on Demand 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="10307-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="10307-199">請與 [Proofpoint on Demand 支援小組](https://www.proofpoint.com/us/support-services)合作，在 Proofpoint on Demand 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="10307-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to add users in the Proofpoint on Demand platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="10307-200">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="10307-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="10307-201">在本節中，您會將 Proofpoint on Demand 的存取權授與 Britta Simon，讓 Britta Simon 能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="10307-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proofpoint on Demand.</span></span>

![指派使用者][200] 

<span data-ttu-id="10307-203">**若要將 Britta Simon 指派到 Proofpoint on Demand，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="10307-203">**To assign Britta Simon to Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="10307-204">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="10307-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="10307-206">在應用程式清單中，選取 [Proofpoint on Demand]。</span><span class="sxs-lookup"><span data-stu-id="10307-206">In the applications list, select **Proofpoint on Demand**.</span></span>

    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="10307-208">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="10307-208">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="10307-210">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="10307-210">Click **Add** button.</span></span> <span data-ttu-id="10307-211">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="10307-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="10307-213">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="10307-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="10307-214">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="10307-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="10307-215">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="10307-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="10307-216">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="10307-216">Testing single sign-on</span></span>

<span data-ttu-id="10307-217">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="10307-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="10307-218">當您在存取面板上按一下 [Proofpoint on Demand] 圖格時，您應該會自動登入 Proofpoint on Demand 應用程式。</span><span class="sxs-lookup"><span data-stu-id="10307-218">When you click the **Proofpoint on Demand** tile on the Access Panel, you should be automatically signed on to your Proofpoint on Demand application.</span></span>
<span data-ttu-id="10307-219">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="10307-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="10307-220">其他資源</span><span class="sxs-lookup"><span data-stu-id="10307-220">Additional resources</span></span>

* [<span data-ttu-id="10307-221">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="10307-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="10307-222">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="10307-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

