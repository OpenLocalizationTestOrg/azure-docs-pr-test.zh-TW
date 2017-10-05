---
title: "教學課程：將 Azure Active Directory 與 Datahug 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Datahug 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: ec431dd5ccfa53e4b975e46da247704dd1e15c2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="d3288-103">教學課程：Azure Active Directory 與 Datahug 整合</span><span class="sxs-lookup"><span data-stu-id="d3288-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="d3288-104">在本教學課程中，您將了解如何整合 Datahug 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d3288-104">In this tutorial, you learn how to integrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3288-105">Datahug 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d3288-105">Integrating Datahug with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3288-106">您可以在 Azure AD 中控制可存取 Datahug 的人員</span><span class="sxs-lookup"><span data-stu-id="d3288-106">You can control in Azure AD who has access to Datahug</span></span>
- <span data-ttu-id="d3288-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Datahug (單一登入)</span><span class="sxs-lookup"><span data-stu-id="d3288-107">You can enable your users to automatically get signed-on to Datahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3288-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d3288-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d3288-109">如果您想要知道與 Azure AD 整合的 SaaS 應用程式詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="d3288-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="d3288-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d3288-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3288-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="d3288-111">Prerequisites</span></span>

<span data-ttu-id="d3288-112">若要設定 Azure AD 與 Datahug 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d3288-112">To configure Azure AD integration with Datahug, you need the following items:</span></span>

- <span data-ttu-id="d3288-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d3288-113">An Azure AD subscription</span></span>
- <span data-ttu-id="d3288-114">啟用 Datahug 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d3288-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3288-115">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d3288-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3288-116">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d3288-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3288-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d3288-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3288-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d3288-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3288-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="d3288-119">Scenario description</span></span>
<span data-ttu-id="d3288-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d3288-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3288-121">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d3288-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3288-122">從資源庫新增 Datahug</span><span class="sxs-lookup"><span data-stu-id="d3288-122">Adding Datahug from the gallery</span></span>
2. <span data-ttu-id="d3288-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d3288-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-the-gallery"></a><span data-ttu-id="d3288-124">從資源庫新增 Datahug</span><span class="sxs-lookup"><span data-stu-id="d3288-124">Adding Datahug from the gallery</span></span>
<span data-ttu-id="d3288-125">若要設定將 Datahug 整合到 Azure AD 中，您需要從資源庫將 Datahug 加入到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="d3288-125">To configure the integration of Datahug into Azure AD, you need to add Datahug from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3288-126">**若要從資源庫新增 Datahug，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d3288-126">**To add Datahug from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3288-127">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d3288-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3288-129">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d3288-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3288-130">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d3288-130">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d3288-132">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d3288-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d3288-134">在搜尋方塊中，輸入 **Datahug**。</span><span class="sxs-lookup"><span data-stu-id="d3288-134">In the search box, type **Datahug**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="d3288-136">在結果窗格中，選取 [Datahug]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3288-136">In the results panel, select **Datahug**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3288-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d3288-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3288-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Datahug 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d3288-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d3288-140">若要讓單一登入運作，Azure AD 必須知道 Datahug 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d3288-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Datahug is to a user in Azure AD.</span></span> <span data-ttu-id="d3288-141">換句話說，必須要建立某位 Azure AD 使用者與 Datahug 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d3288-141">In other words, a link relationship between an Azure AD user and the related user in Datahug needs to be established.</span></span>

<span data-ttu-id="d3288-142">建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值指派為 Datahug 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="d3288-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Datahug.</span></span>

<span data-ttu-id="d3288-143">如要設定及測試搭配 Datahug 的 Azure AD 單一登入，您需要完成下列構成元素：</span><span class="sxs-lookup"><span data-stu-id="d3288-143">To configure and test Azure AD single sign-on with Datahug, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3288-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d3288-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d3288-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d3288-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3288-146">**[建立 Datahug 測試使用者](#creating-a-datahug-test-user)** - 讓 Datahug 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="d3288-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - to have a counterpart of Britta Simon in Datahug that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3288-147">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d3288-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3288-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d3288-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3288-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d3288-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3288-150">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Datahug 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d3288-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="d3288-151">**若要使用 Datahug 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d3288-151">**To configure Azure AD single sign-on with Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="d3288-152">在 Azure 入口網站的 [Datahug] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d3288-152">In the Azure portal, on the **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d3288-154">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="d3288-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="d3288-156">如果您想要以「IDP 起始模式」設定應用程式，請在 [Datahug 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d3288-156">On the **Datahug Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="d3288-158">a.</span><span class="sxs-lookup"><span data-stu-id="d3288-158">a.</span></span> <span data-ttu-id="d3288-159">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="d3288-159">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="d3288-160">b.</span><span class="sxs-lookup"><span data-stu-id="d3288-160">b.</span></span> <span data-ttu-id="d3288-161">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="d3288-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="d3288-162">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="d3288-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="d3288-163">如果您想要以 **SP** 起始模式設定應用程式：</span><span class="sxs-lookup"><span data-stu-id="d3288-163">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="d3288-165">在 [登入 URL] 文字方塊中，將 URL 輸入為：`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="d3288-165">In the **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d3288-166">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="d3288-166">These values are not the real.</span></span> <span data-ttu-id="d3288-167">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="d3288-167">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="d3288-168">在此建議您在 [識別碼] 和 [回覆 URL] 中使用唯一的字串值。</span><span class="sxs-lookup"><span data-stu-id="d3288-168">Here we suggest you to use the unique value of string in the Identifier and Reply URL.</span></span> <span data-ttu-id="d3288-169">請連絡 [Datahug 用戶端支援小組](http://datahug.com/about/contact-us/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="d3288-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) to get these values.</span></span> 

5. <span data-ttu-id="d3288-170">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d3288-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="d3288-172">核取 [顯示進階憑證簽署設定] 並執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d3288-172">Check **“Show advanced certificate signing settings”** and perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="d3288-174">a.</span><span class="sxs-lookup"><span data-stu-id="d3288-174">a.</span></span> <span data-ttu-id="d3288-175">在 [簽署選項] 中，選取 [簽署 SAML 判斷提示]。</span><span class="sxs-lookup"><span data-stu-id="d3288-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="d3288-176">b.</span><span class="sxs-lookup"><span data-stu-id="d3288-176">b.</span></span> <span data-ttu-id="d3288-177">在 [簽署演算法] 中，選取 [SHA1]。</span><span class="sxs-lookup"><span data-stu-id="d3288-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="d3288-178">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d3288-178">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="d3288-180">在 [Datahug 組態] 區段上，按一下 [設定 Datahug] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d3288-180">On the **Datahug Configuration** section, click **Configure Datahug** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d3288-181">從 [快速參考] 區段中複製 [SAML 實體 ID] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="d3288-181">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="d3288-183">若要在 **Datahug** 這一端設定單一登入，您需要將所下載的「中繼資料 XML」、「SAML 實體識別碼」和「SAML 單一登入服務 URL」傳送給 [Datahug 支援小組](http://datahug.com/about/contact-us/)。</span><span class="sxs-lookup"><span data-stu-id="d3288-183">To configure single sign-on on **Datahug** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="d3288-184">他們將會此應用程式設定妥當，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="d3288-184">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d3288-185">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="d3288-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d3288-186">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="d3288-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d3288-187">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d3288-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3288-188">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d3288-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3288-189">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d3288-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d3288-191">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d3288-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3288-192">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d3288-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3288-194">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="d3288-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3288-196">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d3288-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3288-198">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d3288-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3288-200">a.</span><span class="sxs-lookup"><span data-stu-id="d3288-200">a.</span></span> <span data-ttu-id="d3288-201">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d3288-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3288-202">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3288-202">b.</span></span> <span data-ttu-id="d3288-203">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="d3288-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3288-204">c.</span><span class="sxs-lookup"><span data-stu-id="d3288-204">c.</span></span> <span data-ttu-id="d3288-205">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d3288-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d3288-206">d.</span><span class="sxs-lookup"><span data-stu-id="d3288-206">d.</span></span> <span data-ttu-id="d3288-207">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d3288-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="d3288-208">建立 Datahug 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d3288-208">Creating a Datahug test user</span></span>

<span data-ttu-id="d3288-209">若要讓 Azure AD 使用者可以登入 Datahug，則必須將他們佈建到 Datahug。</span><span class="sxs-lookup"><span data-stu-id="d3288-209">To enable Azure AD users to log in to Datahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="d3288-210">在 Datahug 時，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="d3288-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="d3288-211">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d3288-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d3288-212">以系統管理員身分登入您的 Datahug 公司網站。</span><span class="sxs-lookup"><span data-stu-id="d3288-212">Log in to your Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="d3288-213">將滑鼠停留在右上角「齒輪」中，然後按一下 [設定]</span><span class="sxs-lookup"><span data-stu-id="d3288-213">Hover over the **cog** in the top right-hand corner and click **Settings**</span></span>
   
   ![新增員工](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="d3288-215">選擇 [人員]，然後按一下 [新增使用者] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="d3288-215">Choose **People** and click the **Add Users** tab</span></span>

    ![新增員工](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="d3288-217">輸入您想要為其建立帳戶的該人員電子郵件，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d3288-217">Type the email of the person you would like to create an account for and click **Add**.</span></span>

    ![新增員工](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="d3288-219">您也可以選取 [傳送歡迎電子郵件] 核取方塊，將註冊郵件傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="d3288-219">You can send registration mail to user by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="d3288-220">如果您建立的是 Salesforce 帳戶，則不會傳送歡迎電子郵件。</span><span class="sxs-lookup"><span data-stu-id="d3288-220">If you are creating an account for Salesforce do not send the welcome email.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d3288-221">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d3288-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d3288-222">在本節中，您會將 Datahug 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d3288-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Datahug.</span></span>

![指派使用者][200] 

<span data-ttu-id="d3288-224">**若要將 Britta Simon 指派給 Datahug，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d3288-224">**To assign Britta Simon to Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="d3288-225">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d3288-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d3288-227">在應用程式清單中，選取 [Datahug]。</span><span class="sxs-lookup"><span data-stu-id="d3288-227">In the applications list, select **Datahug**.</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="d3288-229">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d3288-229">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d3288-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d3288-231">Click **Add** button.</span></span> <span data-ttu-id="d3288-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d3288-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d3288-234">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="d3288-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d3288-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d3288-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3288-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d3288-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3288-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d3288-237">Testing single sign-on</span></span>

<span data-ttu-id="d3288-238">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="d3288-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="d3288-239">當您在存取面板中按一下 [Datahug] 磚時，應該會自動登入您的 Datahug 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3288-239">When you click the Datahug tile in the Access Panel, you should get automatically signed-on to your Datahug application.</span></span> <span data-ttu-id="d3288-240">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="d3288-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d3288-241">其他資源</span><span class="sxs-lookup"><span data-stu-id="d3288-241">Additional resources</span></span>

* [<span data-ttu-id="d3288-242">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d3288-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3288-243">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d3288-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

