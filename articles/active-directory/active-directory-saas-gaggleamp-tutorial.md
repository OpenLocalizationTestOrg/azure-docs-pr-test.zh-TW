---
title: "教學課程：Azure Active Directory 與 GaggleAMP 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 GaggleAMP 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: c591cf99aecc4153e378c42a530b80deeca63158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="ef072-103">教學課程：Azure Active Directory 與 GaggleAMP 整合</span><span class="sxs-lookup"><span data-stu-id="ef072-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="ef072-104">在本教學課程中，您將了解如何整合 GaggleAMP 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ef072-104">In this tutorial, you learn how to integrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ef072-105">GaggleAMP 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ef072-105">Integrating GaggleAMP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ef072-106">您可以在 Azure AD 中控制可存取 GaggleAMP 的人員</span><span class="sxs-lookup"><span data-stu-id="ef072-106">You can control in Azure AD who has access to GaggleAMP</span></span>
- <span data-ttu-id="ef072-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 GaggleAMP (單一登入)</span><span class="sxs-lookup"><span data-stu-id="ef072-107">You can enable your users to automatically get signed-on to GaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ef072-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="ef072-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ef072-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ef072-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef072-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ef072-110">Prerequisites</span></span>

<span data-ttu-id="ef072-111">若要設定 Azure AD 與 GaggleAMP 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ef072-111">To configure Azure AD integration with GaggleAMP, you need the following items:</span></span>

- <span data-ttu-id="ef072-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ef072-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ef072-113">啟用 GaggleAMP 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ef072-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ef072-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ef072-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ef072-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ef072-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ef072-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ef072-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ef072-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ef072-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ef072-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ef072-118">Scenario description</span></span>
<span data-ttu-id="ef072-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef072-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ef072-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="ef072-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ef072-121">從資源庫新增 GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="ef072-121">Adding GaggleAMP from the gallery</span></span>
2. <span data-ttu-id="ef072-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ef072-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-the-gallery"></a><span data-ttu-id="ef072-123">從資源庫新增 GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="ef072-123">Adding GaggleAMP from the gallery</span></span>
<span data-ttu-id="ef072-124">若要設定將 GaggleAMP 整合到 Azure AD 中，您需要從資源庫將 GaggleAMP 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ef072-124">To configure the integration of GaggleAMP into Azure AD, you need to add GaggleAMP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ef072-125">**若要從資源庫新增 GaggleAMP，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ef072-125">**To add GaggleAMP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ef072-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ef072-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ef072-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ef072-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ef072-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ef072-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ef072-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef072-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ef072-133">在搜尋方塊中，輸入 **GaggleAMP**。</span><span class="sxs-lookup"><span data-stu-id="ef072-133">In the search box, type **GaggleAMP**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="ef072-135">在結果窗格中，選取 [GaggleAMP]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef072-135">In the results panel, select **GaggleAMP**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ef072-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ef072-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ef072-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 GaggleAMP 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef072-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ef072-139">若要讓單一登入運作，Azure AD 必須知道 GaggleAMP 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="ef072-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GaggleAMP is to a user in Azure AD.</span></span> <span data-ttu-id="ef072-140">換句話說，必須建立 Azure AD 使用者和 GaggleAMP 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ef072-140">In other words, a link relationship between an Azure AD user and the related user in GaggleAMP needs to be established.</span></span>

<span data-ttu-id="ef072-141">在 GaggleAMP 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ef072-141">In GaggleAMP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ef072-142">若要設定及測試與 GaggleAMP 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="ef072-142">To configure and test Azure AD single sign-on with GaggleAMP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ef072-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ef072-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ef072-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef072-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ef072-145">**[建立 GaggleAMP 測試使用者](#creating-a-gaggleamp-test-user)** - 在 GaggleAMP 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="ef072-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - to have a counterpart of Britta Simon in GaggleAMP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ef072-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef072-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ef072-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="ef072-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ef072-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ef072-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ef072-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 GaggleAMP 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef072-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="ef072-150">**若要設定與 GaggleAMP 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ef072-150">**To configure Azure AD single sign-on with GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="ef072-151">在 Azure 入口網站的 [GaggleAMP] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ef072-151">In the Azure portal, on the **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ef072-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef072-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="ef072-155">在 [GaggleAMP 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ef072-155">On the **GaggleAMP Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="ef072-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="ef072-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ef072-158">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="ef072-158">The value is not real.</span></span> <span data-ttu-id="ef072-159">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="ef072-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="ef072-160">請連絡 [GaggleAMP 用戶端支援小組](mailto:sales@gaggleamp.com)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="ef072-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) to get the value.</span></span> 
 
4. <span data-ttu-id="ef072-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ef072-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="ef072-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef072-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ef072-165">在 [GaggleAMP 組態] 區段上，按一下 [設定 GaggleAMP] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ef072-165">On the **GaggleAMP Configuration** section, click **Configure GaggleAMP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ef072-166">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="ef072-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="ef072-168">在另一個瀏覽器執行個體中，瀏覽至 Gaggle 支援小組為您建立的 SAML SSO 頁面 (例如：https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit)。</span><span class="sxs-lookup"><span data-stu-id="ef072-168">In another browser instance, navigate to the SAML SSO page created for you by the Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="ef072-169">在您的 [SAML SSO]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ef072-169">On your **SAML SSO** page, perform the following steps:</span></span>  
   
    ![GaggleAMP 單一登入](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="ef072-171">a.</span><span class="sxs-lookup"><span data-stu-id="ef072-171">a.</span></span> <span data-ttu-id="ef072-172">在 [識別提供者簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [簽發者 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="ef072-172">In the **Identity Provider Issuer** textbox, paste the value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="ef072-173">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef072-173">b.</span></span> <span data-ttu-id="ef072-174">在 [識別提供者單一登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="ef072-174">In the **Identity Provider Single Sign-On URL** textbox, paste the  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ef072-175">c.</span><span class="sxs-lookup"><span data-stu-id="ef072-175">c.</span></span> <span data-ttu-id="ef072-176">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="ef072-176">Click **Save**</span></span>      

    <span data-ttu-id="ef072-177">d.</span><span class="sxs-lookup"><span data-stu-id="ef072-177">d.</span></span> <span data-ttu-id="ef072-178">將 [憑證 (Base64)/] 傳送給 [GaggleAMP 支援小組](mailto:sales@gaggleamp.com)。</span><span class="sxs-lookup"><span data-stu-id="ef072-178">Send the **Certificate (Base64)** certificate to your [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="ef072-179">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="ef072-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ef072-180">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="ef072-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ef072-181">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ef072-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ef072-182">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ef072-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="ef072-183">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ef072-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ef072-185">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ef072-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ef072-186">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ef072-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ef072-188">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="ef072-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ef072-190">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ef072-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ef072-192">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ef072-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ef072-194">a.</span><span class="sxs-lookup"><span data-stu-id="ef072-194">a.</span></span> <span data-ttu-id="ef072-195">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ef072-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ef072-196">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef072-196">b.</span></span> <span data-ttu-id="ef072-197">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="ef072-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ef072-198">c.</span><span class="sxs-lookup"><span data-stu-id="ef072-198">c.</span></span> <span data-ttu-id="ef072-199">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="ef072-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ef072-200">d.</span><span class="sxs-lookup"><span data-stu-id="ef072-200">d.</span></span> <span data-ttu-id="ef072-201">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ef072-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="ef072-202">建立 GaggleAMP 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ef072-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="ef072-203">本節的目標是要在 GaggleAMP 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ef072-203">The objective of this section is to create a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="ef072-204">GaggleAMP 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="ef072-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ef072-205">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="ef072-205">There is no action item for you in this section.</span></span> <span data-ttu-id="ef072-206">嘗試存取 GaggleAMP 時，如果使用者尚未存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="ef072-206">A new user is created during an attempt to access GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ef072-207">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ef072-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ef072-208">在本節中，您會將 GaggleAMP 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef072-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GaggleAMP.</span></span>

![指派使用者][200] 

<span data-ttu-id="ef072-210">**若要將 Britta Simon 指派給 GaggleAMP，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ef072-210">**To assign Britta Simon to GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="ef072-211">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ef072-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ef072-213">在應用程式清單中，選取 [GaggleAMP] 。</span><span class="sxs-lookup"><span data-stu-id="ef072-213">In the applications list, select **GaggleAMP**.</span></span>

    ![設定單一登入](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="ef072-215">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ef072-215">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ef072-217">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef072-217">Click **Add** button.</span></span> <span data-ttu-id="ef072-218">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ef072-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ef072-220">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="ef072-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ef072-221">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef072-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ef072-222">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef072-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ef072-223">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ef072-223">Testing single sign-on</span></span>

<span data-ttu-id="ef072-224">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="ef072-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ef072-225">當您在「存取面板」中按一下 [GaggleAMP] 磚時，應該會自動登入您的 GaggleAMP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef072-225">When you click the GaggleAMP tile in the Access Panel, you should get automatically signed-on to your GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ef072-226">其他資源</span><span class="sxs-lookup"><span data-stu-id="ef072-226">Additional resources</span></span>

* [<span data-ttu-id="ef072-227">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="ef072-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ef072-228">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ef072-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

