---
title: "教學課程：Azure Active Directory 與 T&E Express 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 T&E Express 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 869e5284c71904fcc817ceee0f39d94fab1bc6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="0e8be-103">教學課程：Azure Active Directory 與 T&E Express 整合</span><span class="sxs-lookup"><span data-stu-id="0e8be-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="0e8be-104">在本教學課程中，您將了解如何整合 T&E Express 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0e8be-104">In this tutorial, you learn how to integrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e8be-105">T&E Express 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="0e8be-105">Integrating T&E Express with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0e8be-106">您可以在 Azure AD 中控制可存取 T&E Express 的人員</span><span class="sxs-lookup"><span data-stu-id="0e8be-106">You can control in Azure AD who has access to T&E Express</span></span>
- <span data-ttu-id="0e8be-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 T&E Express (單一登入)</span><span class="sxs-lookup"><span data-stu-id="0e8be-107">You can enable your users to automatically get signed-on to T&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e8be-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="0e8be-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="0e8be-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0e8be-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e8be-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0e8be-110">Prerequisites</span></span>

<span data-ttu-id="0e8be-111">若要設定 Azure AD 與 T&E Express 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="0e8be-111">To configure Azure AD integration with T&E Express, you need the following items:</span></span>

- <span data-ttu-id="0e8be-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0e8be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e8be-113">已啟用 T&E Express 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0e8be-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e8be-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0e8be-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e8be-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0e8be-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e8be-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="0e8be-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0e8be-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="0e8be-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e8be-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0e8be-118">Scenario description</span></span>
<span data-ttu-id="0e8be-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e8be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e8be-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="0e8be-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e8be-121">從資源庫新增 T&E Express</span><span class="sxs-lookup"><span data-stu-id="0e8be-121">Adding T&E Express from the gallery</span></span>
2. <span data-ttu-id="0e8be-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0e8be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-the-gallery"></a><span data-ttu-id="0e8be-123">從資源庫新增 T&E Express</span><span class="sxs-lookup"><span data-stu-id="0e8be-123">Adding T&E Express from the gallery</span></span>
<span data-ttu-id="0e8be-124">若要設定將 T&E Express 整合到 Azure AD 中，您需要從資源庫將 T&E Express 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="0e8be-124">To configure the integration of T&E Express into Azure AD, you need to add T&E Express from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0e8be-125">**如要從資源庫新增 T&E Express，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0e8be-125">**To add T&E Express from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0e8be-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0e8be-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e8be-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0e8be-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0e8be-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0e8be-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="0e8be-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e8be-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="0e8be-133">在搜尋方塊中，輸入 **T&E Express**。</span><span class="sxs-lookup"><span data-stu-id="0e8be-133">In the search box, type **T&E Express**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="0e8be-135">在結果窗格中，選取 [T&E Express]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e8be-135">In the results panel, select **T&E Express**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e8be-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0e8be-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e8be-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 T&E Express 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e8be-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e8be-139">若要讓單一登入能夠運作，Azure AD 必須知道 T&E Express 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="0e8be-139">For single sign-on to work, Azure AD needs to know what the counterpart user in T&E Express is to a user in Azure AD.</span></span> <span data-ttu-id="0e8be-140">換句話說，必須在 Azure AD 使用者和 T&E Express 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0e8be-140">In other words, a link relationship between an Azure AD user and the related user in T&E Express needs to be established.</span></span>

<span data-ttu-id="0e8be-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 T&E Express 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="0e8be-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in T&E Express.</span></span>

<span data-ttu-id="0e8be-142">若要使用 T&E Express 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0e8be-142">To configure and test Azure AD single sign-on with T&E Express, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0e8be-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="0e8be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0e8be-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e8be-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e8be-145">**[建立 T&E Express 測試使用者](#creating-a-te-express-test-user)** - 使 T&E Express 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="0e8be-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - to have a counterpart of Britta Simon in T&E Express that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="0e8be-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e8be-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e8be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="0e8be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e8be-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0e8be-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e8be-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 T&E Express 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e8be-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="0e8be-150">**若要設定與 T&E Express 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0e8be-150">**To configure Azure AD single sign-on with T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="0e8be-151">在 Azure 管理入口網站的 [T&E Express] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="0e8be-151">In the Azure Management portal, on the **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="0e8be-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e8be-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="0e8be-155">在 [T&E Express 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0e8be-155">On the **T&E Express Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="0e8be-157">a.</span><span class="sxs-lookup"><span data-stu-id="0e8be-157">a.</span></span> <span data-ttu-id="0e8be-158">在 [識別碼] 文字方塊中，以下列形式輸入值：`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="0e8be-158">In the **Identifier** textbox, type the value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="0e8be-159">b.</span><span class="sxs-lookup"><span data-stu-id="0e8be-159">b.</span></span> <span data-ttu-id="0e8be-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="0e8be-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e8be-161">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="0e8be-161">Please note that these are not the real values.</span></span> <span data-ttu-id="0e8be-162">您必須使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="0e8be-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="0e8be-163">在此建議您在 [識別碼] 中使用唯一的字串值。</span><span class="sxs-lookup"><span data-stu-id="0e8be-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="0e8be-164">請連絡 [T&E Express 支援小組](http://www.tyeexpress.com/contacto.aspx) 以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="0e8be-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) to get these values.</span></span>

5. <span data-ttu-id="0e8be-165">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0e8be-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="0e8be-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e8be-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0e8be-169">若要在 **T&E Express** 端設定單一登入，請使用系統管理員認證而不要使用 SAML 單一登入來登入 T&E Express 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e8be-169">To configure single sign-on on **T&E Express** side, login to the T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="0e8be-170">在 [系統管理員] 索引標籤底下，按一下 [SAML 網域] 以開啟 [SAML 設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="0e8be-170">Under the **Admin** Tab, Click on **SAML domain** to Open the SAML settings page.</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="0e8be-172">將 [Activar (啟動)] 選項從 [No (否)] 改為選取 [SI (是)]。</span><span class="sxs-lookup"><span data-stu-id="0e8be-172">Select the **Activar(Activate)** option from **No** to **SI(Yes)**.</span></span> <span data-ttu-id="0e8be-173">在 [識別提供者中繼資料] 文字方塊中，貼上您從 Azure 入口網站下載的中繼資料 XML。</span><span class="sxs-lookup"><span data-stu-id="0e8be-173">In the **Identity Provider Metadata** textbox, paste the metadata XML which you have donwloaded from Azure portal.</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="0e8be-175">按一下 [Guardar (儲存)] 按鈕以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="0e8be-175">Click on the **Guardar(Save)** button to save the settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e8be-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0e8be-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="0e8be-177">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0e8be-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="0e8be-179">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0e8be-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0e8be-180">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0e8be-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e8be-182">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="0e8be-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e8be-184">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0e8be-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e8be-186">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0e8be-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e8be-188">a.</span><span class="sxs-lookup"><span data-stu-id="0e8be-188">a.</span></span> <span data-ttu-id="0e8be-189">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0e8be-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e8be-190">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e8be-190">b.</span></span> <span data-ttu-id="0e8be-191">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="0e8be-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e8be-192">c.</span><span class="sxs-lookup"><span data-stu-id="0e8be-192">c.</span></span> <span data-ttu-id="0e8be-193">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="0e8be-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0e8be-194">d.</span><span class="sxs-lookup"><span data-stu-id="0e8be-194">d.</span></span> <span data-ttu-id="0e8be-195">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0e8be-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="0e8be-196">建立 T&E Express 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0e8be-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="0e8be-197">若要讓 Azure AD 使用者可以登入 T&E Express，必須將他們佈建到 T&E Express。</span><span class="sxs-lookup"><span data-stu-id="0e8be-197">In order to enable Azure AD users to log into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="0e8be-198">T&E Express 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="0e8be-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="0e8be-199">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0e8be-199">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="0e8be-200">以系統管理員身分登入您的 T&E Express 公司網站。</span><span class="sxs-lookup"><span data-stu-id="0e8be-200">Log in to your T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="0e8be-201">在 [系統管理員] 索引標籤底下，按一下 [使用者] 以開啟 [使用者] 主版頁面。</span><span class="sxs-lookup"><span data-stu-id="0e8be-201">Under Admin tag, click on Users to open the Users master page.</span></span>

    ![新增員工](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="0e8be-203">在首頁上按一下 **+** 以新增使用者。</span><span class="sxs-lookup"><span data-stu-id="0e8be-203">On the home page, click on **+** to add the users.</span></span>

    ![新增員工](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="0e8be-205">在表單中輸入所要求的所有必要詳細資料，然後按一下 [儲存] 按鈕來儲存詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0e8be-205">Enter all the mandatory details as asked in the form and click the save button to save the details.</span></span>

    ![新增員工](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![新增員工](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0e8be-208">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0e8be-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0e8be-209">在本節中，您會將 T&E Express 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e8be-209">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to T&E Express.</span></span>

![指派使用者][200] 

<span data-ttu-id="0e8be-211">**如要將 Britta Simon 指派給 T&E Express，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0e8be-211">**To assign Britta Simon to T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="0e8be-212">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0e8be-212">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0e8be-214">在應用程式清單中，選取 [T&E Express]。</span><span class="sxs-lookup"><span data-stu-id="0e8be-214">In the applications list, select **T&E Express**.</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="0e8be-216">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0e8be-216">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="0e8be-218">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e8be-218">Click **Add** button.</span></span> <span data-ttu-id="0e8be-219">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0e8be-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="0e8be-221">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="0e8be-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0e8be-222">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e8be-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e8be-223">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e8be-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e8be-224">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0e8be-224">Testing single sign-on</span></span>

<span data-ttu-id="0e8be-225">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="0e8be-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0e8be-226">當您在存取面板中按一下 T&E Express 圖格時，應該會自動登入您的 T&E Express 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e8be-226">When you click the T&E Express tile in the Access Panel, you should get automatically signed-on to your T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e8be-227">其他資源</span><span class="sxs-lookup"><span data-stu-id="0e8be-227">Additional resources</span></span>

* [<span data-ttu-id="0e8be-228">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="0e8be-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e8be-229">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0e8be-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

