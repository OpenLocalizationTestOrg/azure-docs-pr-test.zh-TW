---
title: "教學課程：Azure Active Directory 與 IQNavigator VMS 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 IQNavigator VMS 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 1164723a171843541098f6adbda0e65f7e82a0cb
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="6ebf5-103">教學課程：Azure Active Directory 與 IQNavigator VMS 整合</span><span class="sxs-lookup"><span data-stu-id="6ebf5-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="6ebf5-104">在本教學課程中，您會了解如何整合 IQNavigator VMS 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-104">In this tutorial, you learn how to integrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ebf5-105">IQNavigator VMS 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="6ebf5-105">Integrating IQNavigator VMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6ebf5-106">您可以在 Azure AD 中控制可存取 IQNavigator VMS 的人員</span><span class="sxs-lookup"><span data-stu-id="6ebf5-106">You can control in Azure AD who has access to IQNavigator VMS</span></span>
- <span data-ttu-id="6ebf5-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 IQNavigator VMS (單一登入)</span><span class="sxs-lookup"><span data-stu-id="6ebf5-107">You can enable your users to automatically get signed-on to IQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ebf5-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="6ebf5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6ebf5-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ebf5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6ebf5-110">Prerequisites</span></span>

<span data-ttu-id="6ebf5-111">若要設定 Azure AD 與 IQNavigator VMS 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6ebf5-111">To configure Azure AD integration with IQNavigator VMS, you need the following items:</span></span>

- <span data-ttu-id="6ebf5-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6ebf5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ebf5-113">啟用 IQNavigator VMS 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6ebf5-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ebf5-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ebf5-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6ebf5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ebf5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ebf5-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ebf5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6ebf5-118">Scenario description</span></span>
<span data-ttu-id="6ebf5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ebf5-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="6ebf5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ebf5-121">從資源庫新增 IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="6ebf5-121">Adding IQNavigator VMS from the gallery</span></span>
2. <span data-ttu-id="6ebf5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6ebf5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-the-gallery"></a><span data-ttu-id="6ebf5-123">從資源庫新增 IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="6ebf5-123">Adding IQNavigator VMS from the gallery</span></span>
<span data-ttu-id="6ebf5-124">若要設定將 IQNavigator VMS 整合到 Azure AD 中，您需要從資源庫將 IQNavigator VMS 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-124">To configure the integration of IQNavigator VMS into Azure AD, you need to add IQNavigator VMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6ebf5-125">**若要從資源庫新增 IQNavigator VMS，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6ebf5-125">**To add IQNavigator VMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6ebf5-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6ebf5-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6ebf5-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="6ebf5-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="6ebf5-133">在搜尋方塊中，輸入 **IQNavigator VMS**。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-133">In the search box, type **IQNavigator VMS**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="6ebf5-135">在結果面板中，選取 [IQNavigator VMS]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-135">In the results panel, select **IQNavigator VMS**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6ebf5-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6ebf5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6ebf5-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 IQNavigator VMS 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6ebf5-139">若要讓單一登入運作，Azure AD 必須知道 IQNavigator VMS 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IQNavigator VMS is to a user in Azure AD.</span></span> <span data-ttu-id="6ebf5-140">換句話說，必須在 Azure AD 使用者和 IQNavigator VMS 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-140">In other words, a link relationship between an Azure AD user and the related user in IQNavigator VMS needs to be established.</span></span>

<span data-ttu-id="6ebf5-141">在 IQNavigator VMS 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-141">In IQNavigator VMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6ebf5-142">若要設定及測試與 IQNavigator VMS 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6ebf5-142">To configure and test Azure AD single sign-on with IQNavigator VMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6ebf5-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6ebf5-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ebf5-145">**[建立 IQNavigator VMS 測試使用者](#creating-a-iqnavigator-vms-test-user)** - 使 IQNavigator VMS 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - to have a counterpart of Britta Simon in IQNavigator VMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6ebf5-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ebf5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6ebf5-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6ebf5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6ebf5-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 IQNavigator VMS 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="6ebf5-150">**若要設定與 IQNavigator VMS 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6ebf5-150">**To configure Azure AD single sign-on with IQNavigator VMS, perform the following steps:**</span></span>

1. <span data-ttu-id="6ebf5-151">在 Azure 入口網站的 [IQNavigator VMS] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-151">In the Azure portal, on the **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="6ebf5-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="6ebf5-155">在 [IQNavigator VMS 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6ebf5-155">On the **IQNavigator VMS Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="6ebf5-157">a.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-157">a.</span></span> <span data-ttu-id="6ebf5-158">在 [識別碼] 文字方塊中，輸入 URL：`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="6ebf5-158">In the **Identifier** textbox, type the URL:`iqn.com`</span></span>

    <span data-ttu-id="6ebf5-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-159">b.</span></span> <span data-ttu-id="6ebf5-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="6ebf5-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="6ebf5-161">勾選 [顯示進階 URL 設定]，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6ebf5-161">Check **Show advanced URL settings**, perform the following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="6ebf5-163">在 [轉送狀態] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="6ebf5-163">In the **Relay state** textbox, type a URL using the following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6ebf5-164">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-164">These values are not real.</span></span> <span data-ttu-id="6ebf5-165">請使用實際的「回覆 URL」和「轉送狀態」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-165">Update these values with the actual Reply URL and Relay state.</span></span> <span data-ttu-id="6ebf5-166">請連絡 [IQNavigator VMS 客戶支援小組](https://www.beeline.com/iqn-product-support/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) to get these values.</span></span> 

5. <span data-ttu-id="6ebf5-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6ebf5-169">若要產生**中繼資料** URL，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="6ebf5-169">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="6ebf5-170">a.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-170">a.</span></span> <span data-ttu-id="6ebf5-171">按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-171">Click **App registrations**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="6ebf5-173">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-173">b.</span></span> <span data-ttu-id="6ebf5-174">按一下 [端點] 以開啟 [端點] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-174">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="6ebf5-176">c.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-176">c.</span></span> <span data-ttu-id="6ebf5-177">按一下複製按鈕複製 [同盟中繼資料文件] URL，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-177">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="6ebf5-179">d.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-179">d.</span></span> <span data-ttu-id="6ebf5-180">現在，移至 [IQNavigator VMS] 的屬性頁，使用 [複製] 按鈕複製 [應用程式識別碼]，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-180">Now go to the property page of **IQNavigator VMS** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="6ebf5-182">e.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-182">e.</span></span> <span data-ttu-id="6ebf5-183">使用下列模式產生**中繼資料 URL**︰`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="6ebf5-183">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="6ebf5-184">IQNavigator 應用程式需要 [名稱識別碼] 宣告中有唯一的使用者識別碼值。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-184">IQNavigator application expect the unique user identifier value in the Name Identifier claim.</span></span> <span data-ttu-id="6ebf5-185">客戶可以為 [名稱識別碼] 宣告對應正確的值。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-185">Customer can map the correct value for the Name Identifier claim.</span></span> <span data-ttu-id="6ebf5-186">在此案例中，為了示範，我們已對應 user.UserPrincipalName。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-186">In this case we have mapped the user.UserPrincipalName for the demo purpose.</span></span> <span data-ttu-id="6ebf5-187">但是，您應該根據組織的設定，對應正確的值。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-187">But according to your organization settings you should map the correct value for it.</span></span>   

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="6ebf5-189">在 [IQNavigator VMS 組態] 區段上，按一下 [設定 IQNavigator VMS] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-189">On the **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6ebf5-190">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-190">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="6ebf5-192">若要在 **IQNavigator VMS** 端設定單一登入，您必須將**中繼資料 URL**、**登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL** 傳送給 [IQNavigator VMS 支援小組](https://www.beeline.com/iqn-product-support/)。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-192">To configure single sign-on on **IQNavigator VMS** side, you need to send the **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="6ebf5-193">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6ebf5-194">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="6ebf5-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6ebf5-195">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6ebf5-196">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6ebf5-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6ebf5-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6ebf5-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="6ebf5-198">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="6ebf5-200">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6ebf5-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6ebf5-201">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6ebf5-203">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ebf5-205">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ebf5-207">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6ebf5-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6ebf5-209">a.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-209">a.</span></span> <span data-ttu-id="6ebf5-210">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ebf5-211">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-211">b.</span></span> <span data-ttu-id="6ebf5-212">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6ebf5-213">c.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-213">c.</span></span> <span data-ttu-id="6ebf5-214">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6ebf5-215">d.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-215">d.</span></span> <span data-ttu-id="6ebf5-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="6ebf5-217">建立 IQNavigator VM 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6ebf5-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="6ebf5-218">本節的目標是要在 IQNavigator VMS 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-218">The objective of this section is to create a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="6ebf5-219">請與 [IQNavigator VM 支援小組](https://www.beeline.com/iqn-product-support/)合作，在 IQNavigator VM 帳戶中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) to add the users in the IQNavigator VMS account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6ebf5-220">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6ebf5-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6ebf5-221">在本節中，您會將 IQNavigator VMS 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IQNavigator VMS.</span></span>

![指派使用者][200] 

<span data-ttu-id="6ebf5-223">**若要將 Britta Simon 指派給 IQNavigator VMS，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6ebf5-223">**To assign Britta Simon to IQNavigator VMS, perform the following steps:**</span></span>

1. <span data-ttu-id="6ebf5-224">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6ebf5-226">在應用程式清單中，選取 [IQNavigator VMS]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-226">In the applications list, select **IQNavigator VMS**.</span></span>

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="6ebf5-228">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-228">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="6ebf5-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-230">Click **Add** button.</span></span> <span data-ttu-id="6ebf5-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="6ebf5-233">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6ebf5-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ebf5-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6ebf5-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6ebf5-236">Testing single sign-on</span></span>

<span data-ttu-id="6ebf5-237">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6ebf5-238">當您在存取面板中按一下 IQNavigator VMS 圖格時，應該會自動登入您的 IQNavigator VMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-238">When you click the IQNavigator VMS tile in the Access Panel, you should get automatically signed-on to your IQNavigator VMS application.</span></span>
<span data-ttu-id="6ebf5-239">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6ebf5-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ebf5-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="6ebf5-240">Additional resources</span></span>

* [<span data-ttu-id="6ebf5-241">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="6ebf5-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ebf5-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6ebf5-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

