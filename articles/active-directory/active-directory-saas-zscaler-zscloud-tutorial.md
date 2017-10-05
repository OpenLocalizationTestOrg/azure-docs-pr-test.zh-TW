---
title: "教學課程：Azure Active Directory 與 Zscaler ZSCloud 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Zscaler ZSCloud 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 2b6eb113e5725260bc04f50e9218939bf28b1ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="77255-103">教學課程：Azure Active Directory 與 Zscaler ZSCloud 整合</span><span class="sxs-lookup"><span data-stu-id="77255-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="77255-104">在本教學課程中，您將了解如何整合 Zscaler ZSCloud 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="77255-104">In this tutorial, you learn how to integrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77255-105">將 Zscaler ZSCloud 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="77255-105">Integrating Zscaler ZSCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="77255-106">您可以在 Azure AD 中控制可存取 Zscaler ZSCloud 的人員</span><span class="sxs-lookup"><span data-stu-id="77255-106">You can control in Azure AD who has access to Zscaler ZSCloud</span></span>
- <span data-ttu-id="77255-107">您可以讓使用者利用自己的 Azure AD 帳戶，來自動登入 Zscaler ZSCloud (單一登入)</span><span class="sxs-lookup"><span data-stu-id="77255-107">You can enable your users to automatically get signed-on to Zscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77255-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="77255-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="77255-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="77255-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77255-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="77255-110">Prerequisites</span></span>

<span data-ttu-id="77255-111">若要設定 Azure AD 與 Zscaler ZSCloud 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="77255-111">To configure Azure AD integration with Zscaler ZSCloud, you need the following items:</span></span>

- <span data-ttu-id="77255-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="77255-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77255-113">啟用 Zscaler ZSCloud 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="77255-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77255-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="77255-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77255-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="77255-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77255-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="77255-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77255-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="77255-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77255-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="77255-118">Scenario description</span></span>
<span data-ttu-id="77255-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77255-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77255-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="77255-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77255-121">從資源庫新增 Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="77255-121">Adding Zscaler ZSCloud from the gallery</span></span>
2. <span data-ttu-id="77255-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="77255-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-the-gallery"></a><span data-ttu-id="77255-123">從資源庫新增 Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="77255-123">Adding Zscaler ZSCloud from the gallery</span></span>
<span data-ttu-id="77255-124">若要設定將 Zscaler ZSCloud 整合到 Azure AD 中，您需要從資源庫將 Zscaler ZSCloud 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="77255-124">To configure the integration of Zscaler ZSCloud into Azure AD, you need to add Zscaler ZSCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="77255-125">**若要從資源庫新增 Zscaler ZSCloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="77255-125">**To add Zscaler ZSCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="77255-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="77255-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77255-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="77255-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="77255-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="77255-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="77255-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77255-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="77255-133">在搜尋方塊中，鍵入 **Zscaler ZSCloud**。</span><span class="sxs-lookup"><span data-stu-id="77255-133">In the search box, type **Zscaler ZSCloud**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="77255-135">在結果窗格中，選取 [Zscaler ZSCloud]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="77255-135">In the results panel, select **Zscaler ZSCloud**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77255-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="77255-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77255-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Zscaler ZSCloud 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77255-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="77255-139">若要讓單一登入能夠運作，Azure AD 必須知道 Zscaler ZSCloud 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="77255-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler ZSCloud is to a user in Azure AD.</span></span> <span data-ttu-id="77255-140">換句話說，必須在 Azure AD 使用者與 Zscaler ZSCloud 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="77255-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler ZSCloud needs to be established.</span></span>

<span data-ttu-id="77255-141">建立此連結關聯性的方法，就是指派 Azure AD 中**使用者名稱**的值作為 Zscaler ZSCloud 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="77255-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="77255-142">若要使用 Zscaler ZSCloud 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="77255-142">To configure and test Azure AD single sign-on with Zscaler ZSCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="77255-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="77255-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="77255-144">**[設定 Proxy 設定](#configuring-proxy-settings)** - 在 Internet Explorer 中進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="77255-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="77255-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77255-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77255-146">**[建立 Zscaler ZSCloud 測試使用者](#creating-a-zscaler-zscloud-test-user)** - 使 Zscaler ZSCloud 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="77255-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - to have a counterpart of Britta Simon in Zscaler ZSCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="77255-147">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77255-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77255-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="77255-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77255-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="77255-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77255-150">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Zscaler ZSCloud 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="77255-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="77255-151">**若要設定與 Zscaler ZSCloud 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="77255-151">**To configure Azure AD single sign-on with Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="77255-152">在 Azure 入口網站的 [Zscaler ZSCloud] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="77255-152">In the Azure portal, on the **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="77255-154">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="77255-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="77255-156">在 [Zscaler ZSCloud 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="77255-156">On the **Zscaler ZSCloud Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="77255-158">在 [登入 URL] 文字方塊中，鍵入使用者用來登入您 ZScaler ZSCloud 的 URL。</span><span class="sxs-lookup"><span data-stu-id="77255-158">In the **Sign-on URL** textbox, type the URL used by your users to sign-on to your ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="77255-159">您必須使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="77255-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="77255-160">請連絡 [Zscaler ZSCloud 用戶端支援小組](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="77255-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) to get this value.</span></span> 
 
4. <span data-ttu-id="77255-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="77255-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="77255-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="77255-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="77255-165">在 [Zscaler ZSCloud 設定] 區段中，按一下 [設定 Zscaler ZSCloud] 開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="77255-165">On the **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="77255-166">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="77255-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="77255-168">在不同的 Web 瀏覽器視窗中，以管理員身分登入您的 ZScaler ZSCloud 公司網站。</span><span class="sxs-lookup"><span data-stu-id="77255-168">In a different web browser window, log in to your ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="77255-169">在頂端的功能表中，按一下 [系統管理] 。</span><span class="sxs-lookup"><span data-stu-id="77255-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="77255-170">![管理](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "管理")</span><span class="sxs-lookup"><span data-stu-id="77255-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="77255-171">在 [管理系統管理員和角色] 下按一下 [管理使用者和驗證]。</span><span class="sxs-lookup"><span data-stu-id="77255-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="77255-172">![管理使用者和驗證](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "管理使用者和驗證")</span><span class="sxs-lookup"><span data-stu-id="77255-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="77255-173">在 [選擇您的組織的驗證選項]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="77255-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="77255-174">![驗證](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "驗證")</span><span class="sxs-lookup"><span data-stu-id="77255-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="77255-175">a.</span><span class="sxs-lookup"><span data-stu-id="77255-175">a.</span></span> <span data-ttu-id="77255-176">選取 [使用 SAML 單一登入進行驗證] 。</span><span class="sxs-lookup"><span data-stu-id="77255-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="77255-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="77255-177">b.</span></span> <span data-ttu-id="77255-178">按一下 [設定 SAML 單一登入參數] 。</span><span class="sxs-lookup"><span data-stu-id="77255-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="77255-179">在 [設定 SAML 單一登入參數] 對話方塊頁面上，執行下列步驟，然後按一下 [完成]</span><span class="sxs-lookup"><span data-stu-id="77255-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="77255-180">![單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="77255-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="77255-181">a.</span><span class="sxs-lookup"><span data-stu-id="77255-181">a.</span></span> <span data-ttu-id="77255-182">將 [SAML Single Sign-On Service URL] \(SAML 單一登入服務 URL) 值貼到 [URL of the SAML Portal to which users are sent for authentication] \(傳送用於驗證之使用者的 SAML 入口網站 URL) 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="77255-182">Paste the **SAML Single Sign-On Service URL** value into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="77255-183">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="77255-183">b.</span></span> <span data-ttu-id="77255-184">在 [包含登入名稱的屬性] 文字方塊中，輸入 **NameID**。</span><span class="sxs-lookup"><span data-stu-id="77255-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="77255-185">c.</span><span class="sxs-lookup"><span data-stu-id="77255-185">c.</span></span> <span data-ttu-id="77255-186">若要上傳您下載的憑證，請按一下 Zscaler pem 。</span><span class="sxs-lookup"><span data-stu-id="77255-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="77255-187">d.</span><span class="sxs-lookup"><span data-stu-id="77255-187">d.</span></span> <span data-ttu-id="77255-188">選取 [啟用 SAML 自動佈建] 。</span><span class="sxs-lookup"><span data-stu-id="77255-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="77255-189">在 [設定使用者驗證]  對話方塊頁面上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="77255-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="77255-190">![管理](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "管理")</span><span class="sxs-lookup"><span data-stu-id="77255-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="77255-191">a.</span><span class="sxs-lookup"><span data-stu-id="77255-191">a.</span></span> <span data-ttu-id="77255-192">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="77255-192">Click **Save**.</span></span>

    <span data-ttu-id="77255-193">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="77255-193">b.</span></span> <span data-ttu-id="77255-194">按一下 [立即啟用] 。</span><span class="sxs-lookup"><span data-stu-id="77255-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="77255-195">進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="77255-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="77255-196">在 Internet Explorer 中進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="77255-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="77255-197">啟動 **Internet Explorer**。</span><span class="sxs-lookup"><span data-stu-id="77255-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="77255-198">從 [工具] 功能表選取 [網際網路選項] 可開啟 [網際網路選項] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="77255-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="77255-199">![網際網路選項](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "網際網路選項")</span><span class="sxs-lookup"><span data-stu-id="77255-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="77255-200">按一下 [連線]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="77255-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="77255-201">![連線](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "連線")</span><span class="sxs-lookup"><span data-stu-id="77255-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="77255-202">按一下 [區域網路設定] 可開啟 [區域網路設定] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="77255-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="77255-203">在 [Proxy 伺服器] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="77255-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="77255-204">![Proxy 伺服器](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy 伺服器")</span><span class="sxs-lookup"><span data-stu-id="77255-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="77255-205">a.</span><span class="sxs-lookup"><span data-stu-id="77255-205">a.</span></span> <span data-ttu-id="77255-206">選取 [在您的區域網路使用 Proxy 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="77255-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="77255-207">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="77255-207">b.</span></span> <span data-ttu-id="77255-208">在 [位址] 文字方塊中輸入 **gateway.zscalerone.net**。</span><span class="sxs-lookup"><span data-stu-id="77255-208">In the Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="77255-209">c.</span><span class="sxs-lookup"><span data-stu-id="77255-209">c.</span></span> <span data-ttu-id="77255-210">在 [連接埠] 文字方塊中輸入 **80**。</span><span class="sxs-lookup"><span data-stu-id="77255-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="77255-211">d.</span><span class="sxs-lookup"><span data-stu-id="77255-211">d.</span></span> <span data-ttu-id="77255-212">選取 [近端網址不使用 Proxy 伺服器] 。</span><span class="sxs-lookup"><span data-stu-id="77255-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="77255-213">e.</span><span class="sxs-lookup"><span data-stu-id="77255-213">e.</span></span> <span data-ttu-id="77255-214">按一下 [確定] 關閉 [區域網路 (LAN) 設定] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="77255-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="77255-215">按一下 [確定] 關閉 [網際網路選項] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="77255-215">Click **OK** to close the **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77255-216">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="77255-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="77255-217">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="77255-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="77255-219">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="77255-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="77255-220">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="77255-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77255-222">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="77255-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77255-224">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77255-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77255-226">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="77255-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77255-228">a.</span><span class="sxs-lookup"><span data-stu-id="77255-228">a.</span></span> <span data-ttu-id="77255-229">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="77255-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77255-230">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="77255-230">b.</span></span> <span data-ttu-id="77255-231">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="77255-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77255-232">c.</span><span class="sxs-lookup"><span data-stu-id="77255-232">c.</span></span> <span data-ttu-id="77255-233">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="77255-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="77255-234">d.</span><span class="sxs-lookup"><span data-stu-id="77255-234">d.</span></span> <span data-ttu-id="77255-235">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="77255-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="77255-236">建立 Zscaler ZSCloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="77255-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="77255-237">為了讓 Azure AD 使用者登入 ZScaler ZSCloud，他們必須佈建到 ZScaler ZSCloud。</span><span class="sxs-lookup"><span data-stu-id="77255-237">To enable Azure AD users to log in to ZScaler ZSCloud, they must be provisioned to ZScaler ZSCloud.</span></span>  
<span data-ttu-id="77255-238">ZScaler ZSCloud 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="77255-238">In the case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="77255-239">若要設定使用者佈建，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="77255-239">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="77255-240">登入 **Zscaler** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="77255-240">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="77255-241">按一下 [系統管理] 。</span><span class="sxs-lookup"><span data-stu-id="77255-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="77255-242">![管理](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "管理")</span><span class="sxs-lookup"><span data-stu-id="77255-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="77255-243">按一下 [使用者管理] 。</span><span class="sxs-lookup"><span data-stu-id="77255-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="77255-244">![新增](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "新增")</span><span class="sxs-lookup"><span data-stu-id="77255-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="77255-245">在 [使用者] 索引標籤中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77255-245">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="77255-246">![新增](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "新增")</span><span class="sxs-lookup"><span data-stu-id="77255-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="77255-247">在 [新增使用者] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="77255-247">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="77255-248">![新增使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="77255-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="77255-249">a.</span><span class="sxs-lookup"><span data-stu-id="77255-249">a.</span></span> <span data-ttu-id="77255-250">輸入 [使用者識別碼]、[使用者顯示名稱]、[密碼]、[確認密碼]，然後選取您要佈建之有效 AAD 帳戶的 [群組] 和 [部門]。</span><span class="sxs-lookup"><span data-stu-id="77255-250">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="77255-251">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="77255-251">b.</span></span> <span data-ttu-id="77255-252">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="77255-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="77255-253">您可以使用任何其他的 ZScaler ZSCloud 使用者帳戶建立工具或 ZScaler ZSCloud 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="77255-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="77255-254">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="77255-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="77255-255">在本節中，您會將 Zscaler ZSCloud 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77255-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler ZSCloud.</span></span>

![指派使用者][200] 

<span data-ttu-id="77255-257">**若要指派 Britta Simon 給 ZScaler ZSCloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="77255-257">**To assign Britta Simon to Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="77255-258">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="77255-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="77255-260">在應用程式清單中，選取 [Zscaler ZSCloud]。</span><span class="sxs-lookup"><span data-stu-id="77255-260">In the applications list, select **Zscaler ZSCloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="77255-262">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="77255-262">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="77255-264">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77255-264">Click **Add** button.</span></span> <span data-ttu-id="77255-265">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="77255-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="77255-267">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="77255-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="77255-268">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77255-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77255-269">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77255-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77255-270">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="77255-270">Testing single sign-on</span></span>

<span data-ttu-id="77255-271">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="77255-271">If you want to test your single sign-on settings, open the Access Panel.</span></span>

<span data-ttu-id="77255-272">當您在存取面板中按一下 [Zscaler ZSCloud] 磚時，應該會自動登入您的 Zscaler ZSCloud 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77255-272">When you click the Zscaler ZSCloud tile in the Access Panel, you should get automatically signed-on to your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="77255-273">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="77255-273">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="77255-274">其他資源</span><span class="sxs-lookup"><span data-stu-id="77255-274">Additional resources</span></span>

* [<span data-ttu-id="77255-275">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="77255-275">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77255-276">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="77255-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png
