---
title: "教學課程：Azure Active Directory 與 Sugar CRM 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Sugar CRM 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c27aef24e859522b8001ecb747906abdca14d87a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="527ba-103">教學課程：Azure Active Directory 與 Sugar CRM 整合</span><span class="sxs-lookup"><span data-stu-id="527ba-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="527ba-104">在本教學課程中，您會了解如何將 Sugar CRM 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="527ba-104">In this tutorial, you learn how to integrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="527ba-105">Sugar CRM 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="527ba-105">Integrating Sugar CRM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="527ba-106">您可以在 Azure AD 中管控可存取 Sugar CRM 的人員</span><span class="sxs-lookup"><span data-stu-id="527ba-106">You can control in Azure AD who has access to Sugar CRM</span></span>
- <span data-ttu-id="527ba-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Sugar CRM (單一登入)</span><span class="sxs-lookup"><span data-stu-id="527ba-107">You can enable your users to automatically get signed-on to Sugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="527ba-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="527ba-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="527ba-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="527ba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="527ba-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="527ba-110">Prerequisites</span></span>

<span data-ttu-id="527ba-111">若要設定 Azure AD 與 Sugar CRM 的整合作業，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="527ba-111">To configure Azure AD integration with Sugar CRM, you need the following items:</span></span>

- <span data-ttu-id="527ba-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="527ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="527ba-113">已啟用 Sugar CRM 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="527ba-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="527ba-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="527ba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="527ba-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="527ba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="527ba-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="527ba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="527ba-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="527ba-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="527ba-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="527ba-118">Scenario description</span></span>
<span data-ttu-id="527ba-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="527ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="527ba-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="527ba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="527ba-121">從資源庫新增 Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="527ba-121">Adding Sugar CRM from the gallery</span></span>
2. <span data-ttu-id="527ba-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="527ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-the-gallery"></a><span data-ttu-id="527ba-123">從資源庫新增 Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="527ba-123">Adding Sugar CRM from the gallery</span></span>
<span data-ttu-id="527ba-124">若要設定 Sugar CRM 與 Azure AD 整合，您需要從資源庫將 Sugar CRM 加入受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="527ba-124">To configure the integration of Sugar CRM into Azure AD, you need to add Sugar CRM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="527ba-125">**若要從資源庫新增 Sugar CRM，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="527ba-125">**To add Sugar CRM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="527ba-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="527ba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="527ba-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="527ba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="527ba-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="527ba-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="527ba-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="527ba-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="527ba-133">在搜尋方塊中，輸入 **Sugar CRM**。</span><span class="sxs-lookup"><span data-stu-id="527ba-133">In the search box, type **Sugar CRM**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="527ba-135">在結果窗格中，選取 [Sugar CRM]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="527ba-135">In the results panel, select **Sugar CRM**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="527ba-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="527ba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="527ba-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Sugar CRM 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="527ba-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="527ba-139">若要讓單一登入運作，Azure AD 必須知道 Sugar CRM 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="527ba-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sugar CRM is to a user in Azure AD.</span></span> <span data-ttu-id="527ba-140">換句話說，必須在 Azure AD 使用者和 Sugar CRM 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="527ba-140">In other words, a link relationship between an Azure AD user and the related user in Sugar CRM needs to be established.</span></span>

<span data-ttu-id="527ba-141">在 Sugar CRM 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="527ba-141">In Sugar CRM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="527ba-142">若要使用 Sugar CRM 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="527ba-142">To configure and test Azure AD single sign-on with Sugar CRM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="527ba-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="527ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="527ba-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="527ba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="527ba-145">**[建立 Sugar CRM 測試使用者](#creating-a-sugar-crm-test-user)** - 使 Sugar CRM 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="527ba-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - to have a counterpart of Britta Simon in Sugar CRM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="527ba-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="527ba-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="527ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="527ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="527ba-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="527ba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="527ba-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Sugar CRM 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="527ba-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="527ba-150">**若要使用 Sugar CRM 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="527ba-150">**To configure Azure AD single sign-on with Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="527ba-151">在 Azure 入口網站的 [Sugar CRM] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="527ba-151">In the Azure portal, on the **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="527ba-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="527ba-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="527ba-155">在 [Sugar CRM 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="527ba-155">On the **Sugar CRM Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="527ba-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰</span><span class="sxs-lookup"><span data-stu-id="527ba-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="527ba-158">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="527ba-158">The value is not real.</span></span> <span data-ttu-id="527ba-159">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="527ba-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="527ba-160">請連絡 [Sugar CRM 客戶支援小組](https://support.sugarcrm.com/)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="527ba-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="527ba-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="527ba-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="527ba-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="527ba-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="527ba-165">在 [Sugar CRM 組態] 區段上，按一下 [設定 Sugar CRM] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="527ba-165">On the **Sugar CRM Configuration** section, click **Configure Sugar CRM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="527ba-166">從 [快速參考] 區段中複製 [登入 URL] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="527ba-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="527ba-168">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Sugar CRM 公司網站。</span><span class="sxs-lookup"><span data-stu-id="527ba-168">In a different web browser window, log in to your Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="527ba-169">移至 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="527ba-169">Go to **Admin**.</span></span>
   
    <span data-ttu-id="527ba-170">![管理](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "管理")</span><span class="sxs-lookup"><span data-stu-id="527ba-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="527ba-171">在 [管理] 區段中，按一下 [密碼管理]。</span><span class="sxs-lookup"><span data-stu-id="527ba-171">In the **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="527ba-172">![管理](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "管理")</span><span class="sxs-lookup"><span data-stu-id="527ba-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="527ba-173">按一下 [啟用 SAML 驗證]。</span><span class="sxs-lookup"><span data-stu-id="527ba-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="527ba-174">![管理](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "管理")</span><span class="sxs-lookup"><span data-stu-id="527ba-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="527ba-175">在 [SAML 驗證]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="527ba-175">In the **SAML Authentication** section, perform the following steps:</span></span>
   
    <span data-ttu-id="527ba-176">![SAML 驗證](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML 驗證")</span><span class="sxs-lookup"><span data-stu-id="527ba-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="527ba-177">a.</span><span class="sxs-lookup"><span data-stu-id="527ba-177">a.</span></span> <span data-ttu-id="527ba-178">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="527ba-178">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="527ba-179">b.</span><span class="sxs-lookup"><span data-stu-id="527ba-179">b.</span></span> <span data-ttu-id="527ba-180">在 [SLO URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="527ba-180">In the **SLO URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="527ba-181">c.</span><span class="sxs-lookup"><span data-stu-id="527ba-181">c.</span></span> <span data-ttu-id="527ba-182">在記事本中開啟您的 base-64 編碼的憑證，將它的內容複製到您的剪貼簿，然後將整個憑證貼到 [X.509 憑證]  文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="527ba-182">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="527ba-183">d.</span><span class="sxs-lookup"><span data-stu-id="527ba-183">d.</span></span> <span data-ttu-id="527ba-184">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="527ba-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="527ba-185">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="527ba-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="527ba-186">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="527ba-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="527ba-187">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="527ba-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="527ba-188">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="527ba-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="527ba-189">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="527ba-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="527ba-191">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="527ba-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="527ba-192">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="527ba-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="527ba-194">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="527ba-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="527ba-196">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="527ba-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="527ba-198">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="527ba-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="527ba-200">a.</span><span class="sxs-lookup"><span data-stu-id="527ba-200">a.</span></span> <span data-ttu-id="527ba-201">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="527ba-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="527ba-202">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="527ba-202">b.</span></span> <span data-ttu-id="527ba-203">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="527ba-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="527ba-204">c.</span><span class="sxs-lookup"><span data-stu-id="527ba-204">c.</span></span> <span data-ttu-id="527ba-205">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="527ba-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="527ba-206">d.</span><span class="sxs-lookup"><span data-stu-id="527ba-206">d.</span></span> <span data-ttu-id="527ba-207">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="527ba-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="527ba-208">建立 Sugar CRM 測試使用者</span><span class="sxs-lookup"><span data-stu-id="527ba-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="527ba-209">若要讓 Azure AD 使用者能夠登入 Sugar CRM，必須將他們佈建到 Sugar CRM。</span><span class="sxs-lookup"><span data-stu-id="527ba-209">In order to enable Azure AD users to log in to Sugar CRM, they must be provisioned to Sugar CRM.</span></span>

<span data-ttu-id="527ba-210">Sugar CRM 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="527ba-210">In the case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="527ba-211">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="527ba-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="527ba-212">以系統管理員身分登入您的 **Sugar CRM** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="527ba-212">Log in to your **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="527ba-213">移至 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="527ba-213">Go to **Admin**.</span></span>
   
    <span data-ttu-id="527ba-214">![管理](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "管理")</span><span class="sxs-lookup"><span data-stu-id="527ba-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="527ba-215">在 [管理] 區段中，按一下 [使用者管理]。</span><span class="sxs-lookup"><span data-stu-id="527ba-215">In the **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="527ba-216">![管理](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "管理")</span><span class="sxs-lookup"><span data-stu-id="527ba-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="527ba-217">移至 [使用者] \> [建立新的使用者]。</span><span class="sxs-lookup"><span data-stu-id="527ba-217">Go to **Users \> Create New User**.</span></span>
   
    <span data-ttu-id="527ba-218">![建立新的使用者](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "建立新的使用者")</span><span class="sxs-lookup"><span data-stu-id="527ba-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="527ba-219">在 [使用者設定檔]  索引標籤上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="527ba-219">On the **User Profile** tab, perform the following steps:</span></span>
   
    <span data-ttu-id="527ba-220">![新增使用者](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="527ba-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="527ba-221">a.</span><span class="sxs-lookup"><span data-stu-id="527ba-221">a.</span></span> <span data-ttu-id="527ba-222">在相關的文字方塊中，輸入有效 Azure Active Directory 使用者的**使用者名稱**、**姓氏**和**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="527ba-222">Type the **user name**, **last name**, and **email address** of a valid Azure Active Directory user into the related textboxes.</span></span>
  
6. <span data-ttu-id="527ba-223">在 [狀態] 選取 [作用中]。</span><span class="sxs-lookup"><span data-stu-id="527ba-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="527ba-224">在 [密碼] 索引標籤上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="527ba-224">On the Password tab, perform the following steps:</span></span>
   
    <span data-ttu-id="527ba-225">![新增使用者](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="527ba-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="527ba-226">a.</span><span class="sxs-lookup"><span data-stu-id="527ba-226">a.</span></span> <span data-ttu-id="527ba-227">在相關的文字方塊中輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="527ba-227">Type the password into the related textbox.</span></span>

    <span data-ttu-id="527ba-228">b.</span><span class="sxs-lookup"><span data-stu-id="527ba-228">b.</span></span> <span data-ttu-id="527ba-229">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="527ba-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="527ba-230">您可以使用任何其他的 Sugar CRM 使用者帳戶建立工具或 Sugar CRM 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="527ba-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="527ba-231">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="527ba-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="527ba-232">在本節中，您會將 Sugar CRM 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="527ba-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sugar CRM.</span></span>

![指派使用者][200] 

<span data-ttu-id="527ba-234">**若要將 Britta Simon 指派給 Sugar CRM，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="527ba-234">**To assign Britta Simon to Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="527ba-235">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="527ba-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="527ba-237">在應用程式清單中，選取 [Sugar CRM]。</span><span class="sxs-lookup"><span data-stu-id="527ba-237">In the applications list, select **Sugar CRM**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="527ba-239">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="527ba-239">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="527ba-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="527ba-241">Click **Add** button.</span></span> <span data-ttu-id="527ba-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="527ba-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="527ba-244">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="527ba-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="527ba-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="527ba-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="527ba-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="527ba-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="527ba-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="527ba-247">Testing single sign-on</span></span>

<span data-ttu-id="527ba-248">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="527ba-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="527ba-249">當您在存取面板中按一下 [Sugar CRM] 圖格時，應該會自動登入您的 Sugar CRM 應用程式。</span><span class="sxs-lookup"><span data-stu-id="527ba-249">When you click the Sugar CRM tile in the Access Panel, you should get automatically signed-on to your Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="527ba-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="527ba-250">Additional resources</span></span>

* [<span data-ttu-id="527ba-251">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="527ba-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="527ba-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="527ba-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

