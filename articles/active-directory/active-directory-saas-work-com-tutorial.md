---
title: "教學課程：Azure Active Directory 與 Work.com 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Work.com 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 7cfec8e9ac12d43095483696a15c0580776d3114
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="3a387-103">教學課程：Azure Active Directory 與 Work.com 整合</span><span class="sxs-lookup"><span data-stu-id="3a387-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="3a387-104">在本教學課程中，您將了解如何整合 Work.com 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="3a387-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a387-105">Work.com 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="3a387-105">Integrating Work.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3a387-106">您可以在 Azure AD 中控制可存取 Work.com 的人員</span><span class="sxs-lookup"><span data-stu-id="3a387-106">You can control in Azure AD who has access to Work.com</span></span>
- <span data-ttu-id="3a387-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Work.com (單一登入)</span><span class="sxs-lookup"><span data-stu-id="3a387-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a387-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="3a387-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3a387-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3a387-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a387-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3a387-110">Prerequisites</span></span>

<span data-ttu-id="3a387-111">若要設定 Azure AD 與 Work.com 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="3a387-111">To configure Azure AD integration with Work.com, you need the following items:</span></span>

- <span data-ttu-id="3a387-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3a387-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a387-113">已啟用 Work.com 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3a387-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a387-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3a387-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a387-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3a387-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a387-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3a387-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a387-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="3a387-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a387-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="3a387-118">Scenario description</span></span>
<span data-ttu-id="3a387-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a387-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a387-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="3a387-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a387-121">從資源庫新增 Work.com</span><span class="sxs-lookup"><span data-stu-id="3a387-121">Add Work.com from the gallery</span></span>
2. <span data-ttu-id="3a387-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3a387-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-the-gallery"></a><span data-ttu-id="3a387-123">從資源庫新增 Work.com</span><span class="sxs-lookup"><span data-stu-id="3a387-123">Add Work.com from the gallery</span></span>
<span data-ttu-id="3a387-124">若要設定將 Work.com 整合到 Azure AD 中，您需要從資源庫將 Work.com 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="3a387-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3a387-125">**若要從資源庫新增 Work.com，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3a387-125">**To add Work.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3a387-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3a387-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3a387-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3a387-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3a387-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3a387-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="3a387-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a387-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="3a387-133">在搜尋方塊中，輸入 **Work.com**，從結果面板中選取 [Work.com]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a387-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span></span>

    ![從資源庫新增](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3a387-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3a387-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3a387-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Work.com 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a387-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3a387-137">若要讓單一登入運作，Azure AD 必須知道 Work.com 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="3a387-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span></span> <span data-ttu-id="3a387-138">換句話說，必須在 Azure AD 使用者和 Work.com 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3a387-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span></span>

<span data-ttu-id="3a387-139">在 Work.com 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3a387-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3a387-140">若要設定及測試與 Work.com 搭配運作的 Azure AD 單一登入，您需要完成下列建構元素：</span><span class="sxs-lookup"><span data-stu-id="3a387-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3a387-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="3a387-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3a387-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a387-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a387-143">**[建立 Work.com 測試使用者](#create-a-workcom-test-user)** - 使Work.com 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="3a387-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a387-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a387-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a387-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="3a387-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3a387-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3a387-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3a387-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Work.com 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a387-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="3a387-148">若要設定單一登入，您還需要設定自訂的 Work.com 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="3a387-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="3a387-149">您至少需要定義一個網域名稱、測試網域名稱，並將它部署到整個組織。</span><span class="sxs-lookup"><span data-stu-id="3a387-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>

<span data-ttu-id="3a387-150">**若要使用 Work.com 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3a387-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="3a387-151">在 Azure 入口網站的 [Work.com] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="3a387-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="3a387-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a387-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="3a387-155">在 [Work.com 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3a387-155">On the **Work.com Domain and URLs** section, perform the following:</span></span>

    ![[Work.com 網域與 URL] 區段](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="3a387-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="3a387-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3a387-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="3a387-158">This value is not real.</span></span> <span data-ttu-id="3a387-159">請使用實際的登入 URL 來更新此值。</span><span class="sxs-lookup"><span data-stu-id="3a387-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3a387-160">請連絡 [Work.com 用戶端支援小組](https://help.salesforce.com/articleView?id=000159855&type=3)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="3a387-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span></span> 

4. <span data-ttu-id="3a387-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="3a387-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="3a387-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a387-163">Click **Save** button.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3a387-165">在 [Work.com 設定] 區段上，按一下 [設定 Work.com] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="3a387-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3a387-166">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="3a387-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![[Work.com 設定] 區段](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="3a387-168">以系統管理員身分登入 Work.com 租用戶。</span><span class="sxs-lookup"><span data-stu-id="3a387-168">Log in to your Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="3a387-169">移到 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="3a387-169">Go to **Setup**.</span></span>
   
    <span data-ttu-id="3a387-170">![設定](./media/active-directory-saas-work-com-tutorial/ic794108.png "設定")</span><span class="sxs-lookup"><span data-stu-id="3a387-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="3a387-171">在 [系統管理員] 區段的左方導覽窗格中，按一下 [網域管理] 展開相關的區段，然後按一下 [我的網域] 來開啟 [我的網域] 頁面。</span><span class="sxs-lookup"><span data-stu-id="3a387-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="3a387-172">![我的網域](./media/active-directory-saas-work-com-tutorial/ic767825.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="3a387-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="3a387-173">若要確認已正確設定您的網域，請確定目前在 [步驟 4 已部署到使用者] 中，然後檢閱 [我的網域設定]。</span><span class="sxs-lookup"><span data-stu-id="3a387-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="3a387-174">![已部署到使用者的網域](./media/active-directory-saas-work-com-tutorial/ic784377.png "已部署到使用者的網域")</span><span class="sxs-lookup"><span data-stu-id="3a387-174">![Domain Deployed to User](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="3a387-175">登入 Work.com 租用戶。</span><span class="sxs-lookup"><span data-stu-id="3a387-175">Log in to your Work.com tenant.</span></span>

12. <span data-ttu-id="3a387-176">移到 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="3a387-176">Go to **Setup**.</span></span>
    
    <span data-ttu-id="3a387-177">![設定](./media/active-directory-saas-work-com-tutorial/ic794108.png "設定")</span><span class="sxs-lookup"><span data-stu-id="3a387-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="3a387-178">展開 [安全性控制] 功能表，然後再按一下 [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="3a387-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="3a387-179">![單一登入設定](./media/active-directory-saas-work-com-tutorial/ic794113.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="3a387-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="3a387-180">在 [單一登入設定]  對話方塊頁面執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3a387-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="3a387-181">![啟用 SAML](./media/active-directory-saas-work-com-tutorial/ic781026.png "啟用 SAML")</span><span class="sxs-lookup"><span data-stu-id="3a387-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="3a387-182">a.</span><span class="sxs-lookup"><span data-stu-id="3a387-182">a.</span></span> <span data-ttu-id="3a387-183">選取 [已啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="3a387-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="3a387-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a387-184">b.</span></span> <span data-ttu-id="3a387-185">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="3a387-185">Click **New**.</span></span>

15. <span data-ttu-id="3a387-186">在 [SAML 單一登入設定]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3a387-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="3a387-187">![SAML 單一登入設定](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML 單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="3a387-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="3a387-188">a.</span><span class="sxs-lookup"><span data-stu-id="3a387-188">a.</span></span> <span data-ttu-id="3a387-189">在 [名稱]  文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="3a387-189">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="3a387-190">提供 [名稱] 的值，[API 名稱] 文字方塊就會自動填入內容。</span><span class="sxs-lookup"><span data-stu-id="3a387-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    
    <span data-ttu-id="3a387-191">b.</span><span class="sxs-lookup"><span data-stu-id="3a387-191">b.</span></span> <span data-ttu-id="3a387-192">在 [簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="3a387-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="3a387-193">c.</span><span class="sxs-lookup"><span data-stu-id="3a387-193">c.</span></span> <span data-ttu-id="3a387-194">若要上傳從 Azure 入口網站下載的憑證，請按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="3a387-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="3a387-195">d.</span><span class="sxs-lookup"><span data-stu-id="3a387-195">d.</span></span> <span data-ttu-id="3a387-196">在 [實體識別碼] 文字方塊中，輸入 `https://salesforce-work.com`。</span><span class="sxs-lookup"><span data-stu-id="3a387-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="3a387-197">e.</span><span class="sxs-lookup"><span data-stu-id="3a387-197">e.</span></span> <span data-ttu-id="3a387-198">對於 [SAML 身分識別類型]，選取 [判斷提示包含來自使用者物件的同盟識別碼]。</span><span class="sxs-lookup"><span data-stu-id="3a387-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="3a387-199">f.</span><span class="sxs-lookup"><span data-stu-id="3a387-199">f.</span></span> <span data-ttu-id="3a387-200">在 [SAML 識別位置]，請選取 [識別位於 Subject 陳述式的 NameIdentifier 元素中]。</span><span class="sxs-lookup"><span data-stu-id="3a387-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="3a387-201">g.</span><span class="sxs-lookup"><span data-stu-id="3a387-201">g.</span></span> <span data-ttu-id="3a387-202">在 [識別提供者登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="3a387-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3a387-203">h.</span><span class="sxs-lookup"><span data-stu-id="3a387-203">h.</span></span> <span data-ttu-id="3a387-204">在 [識別提供者登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="3a387-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="3a387-205">i.</span><span class="sxs-lookup"><span data-stu-id="3a387-205">i.</span></span> <span data-ttu-id="3a387-206">在 [服務提供者起始的要求繫結]，選取 [HTTP Post]。</span><span class="sxs-lookup"><span data-stu-id="3a387-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="3a387-207">j.</span><span class="sxs-lookup"><span data-stu-id="3a387-207">j.</span></span> <span data-ttu-id="3a387-208">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3a387-208">Click **Save**.</span></span>

16. <span data-ttu-id="3a387-209">在 Work.com 傳統入口網站的左側導覽窗格中，按一下 [網域管理] 以展開相關區段，然後按一下 [我的網域] 來開啟 [我的網域] 頁面。</span><span class="sxs-lookup"><span data-stu-id="3a387-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="3a387-210">![我的網域](./media/active-directory-saas-work-com-tutorial/ic794115.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="3a387-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="3a387-211">在 [我的網域] 頁面的 [登入頁面商標] 區段中，按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="3a387-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="3a387-212">![登入頁面商標](./media/active-directory-saas-work-com-tutorial/ic767826.png "登入頁面商標")</span><span class="sxs-lookup"><span data-stu-id="3a387-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="3a387-213">[登入頁面商標] 頁面的 [驗證服務] 區段中，會顯示您的 [SAML SSO 設定] 的名稱。</span><span class="sxs-lookup"><span data-stu-id="3a387-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="3a387-214">請選取該名稱，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3a387-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="3a387-215">![登入頁面商標](./media/active-directory-saas-work-com-tutorial/ic784366.png "登入頁面商標")</span><span class="sxs-lookup"><span data-stu-id="3a387-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="3a387-216">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="3a387-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3a387-217">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="3a387-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3a387-218">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a387-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3a387-219">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3a387-219">Create an Azure AD test user</span></span>
<span data-ttu-id="3a387-220">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3a387-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="3a387-222">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3a387-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3a387-223">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3a387-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a387-225">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="3a387-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] -> [所有使用者]](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a387-227">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="3a387-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![加](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a387-229">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3a387-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![使用者對話方塊頁面](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a387-231">a.</span><span class="sxs-lookup"><span data-stu-id="3a387-231">a.</span></span> <span data-ttu-id="3a387-232">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3a387-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a387-233">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a387-233">b.</span></span> <span data-ttu-id="3a387-234">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="3a387-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3a387-235">c.</span><span class="sxs-lookup"><span data-stu-id="3a387-235">c.</span></span> <span data-ttu-id="3a387-236">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="3a387-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3a387-237">d.</span><span class="sxs-lookup"><span data-stu-id="3a387-237">d.</span></span> <span data-ttu-id="3a387-238">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3a387-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="3a387-239">建立 Work.com 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3a387-239">Create a Work.com test user</span></span>
<span data-ttu-id="3a387-240">Azure Active Directory 使用者必須先佈建到 Work.com，才可以登入。</span><span class="sxs-lookup"><span data-stu-id="3a387-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span> <span data-ttu-id="3a387-241">Work.com 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="3a387-241">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="3a387-242">若要設定使用者佈建，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3a387-242">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="3a387-243">以系統管理員身分登入您的 Work.com 公司網站。</span><span class="sxs-lookup"><span data-stu-id="3a387-243">Sign on to your Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="3a387-244">移到 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="3a387-244">Go to **Setup**.</span></span>
   
    <span data-ttu-id="3a387-245">![設定](./media/active-directory-saas-work-com-tutorial/IC794108.png "設定")</span><span class="sxs-lookup"><span data-stu-id="3a387-245">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="3a387-246">移至 [管理使用者 \> 使用者]。</span><span class="sxs-lookup"><span data-stu-id="3a387-246">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="3a387-247">![管理使用者](./media/active-directory-saas-work-com-tutorial/IC784369.png "管理使用者")</span><span class="sxs-lookup"><span data-stu-id="3a387-247">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="3a387-248">按一下 [新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="3a387-248">Click **New User**.</span></span>
   
    <span data-ttu-id="3a387-249">![所有使用者](./media/active-directory-saas-work-com-tutorial/IC794117.png "所有使用者")</span><span class="sxs-lookup"><span data-stu-id="3a387-249">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="3a387-250">在 [使用者編輯] 區段中，在您想要佈建至相關文字方塊之有效 Azure AD 帳戶的屬性中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3a387-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span></span>
   
    <span data-ttu-id="3a387-251">![使用者編輯](./media/active-directory-saas-work-com-tutorial/ic794118.png "使用者編輯")</span><span class="sxs-lookup"><span data-stu-id="3a387-251">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="3a387-252">a.</span><span class="sxs-lookup"><span data-stu-id="3a387-252">a.</span></span> <span data-ttu-id="3a387-253">在 [名字] 文字方塊中，輸入使用者的**名字**：**Britta**。</span><span class="sxs-lookup"><span data-stu-id="3a387-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span></span>
    
    <span data-ttu-id="3a387-254">b.</span><span class="sxs-lookup"><span data-stu-id="3a387-254">b.</span></span> <span data-ttu-id="3a387-255">在 [姓氏] 文字方塊中，輸入使用者的**姓氏**：**Simon**。</span><span class="sxs-lookup"><span data-stu-id="3a387-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span></span>
    
    <span data-ttu-id="3a387-256">c.</span><span class="sxs-lookup"><span data-stu-id="3a387-256">c.</span></span> <span data-ttu-id="3a387-257">在 [別名] 文字方塊中，輸入使用者的**名字**：**BrittaS**。</span><span class="sxs-lookup"><span data-stu-id="3a387-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span></span>
    
    <span data-ttu-id="3a387-258">d.</span><span class="sxs-lookup"><span data-stu-id="3a387-258">d.</span></span> <span data-ttu-id="3a387-259">在 [電子郵件] 文字方塊中，輸入使用者 **Brittasimon@contoso.com** 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="3a387-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="3a387-260">e.</span><span class="sxs-lookup"><span data-stu-id="3a387-260">e.</span></span> <span data-ttu-id="3a387-261">在 [使用者名稱] 文字方塊中，輸入使用者的使用者名稱，例如 **Brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="3a387-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="3a387-262">f.</span><span class="sxs-lookup"><span data-stu-id="3a387-262">f.</span></span> <span data-ttu-id="3a387-263">在 [暱稱] 文字方塊中，輸入使用者的**暱稱**：**Simon**。</span><span class="sxs-lookup"><span data-stu-id="3a387-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="3a387-264">g.</span><span class="sxs-lookup"><span data-stu-id="3a387-264">g.</span></span> <span data-ttu-id="3a387-265">選取 [角色]、[使用者授權] 和 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="3a387-265">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="3a387-266">h.</span><span class="sxs-lookup"><span data-stu-id="3a387-266">h.</span></span> <span data-ttu-id="3a387-267">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3a387-267">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="3a387-268">Azure AD 帳戶的持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="3a387-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3a387-269">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3a387-269">Assign the Azure AD test user</span></span>

<span data-ttu-id="3a387-270">在本節中，您會將 Work.com 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a387-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span></span>

![指派使用者][200] 

<span data-ttu-id="3a387-272">**若要將 Britta Simon 指派給 Work.com，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3a387-272">**To assign Britta Simon to Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="3a387-273">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3a387-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3a387-275">在應用程式清單中，選取 [Work.com]。</span><span class="sxs-lookup"><span data-stu-id="3a387-275">In the applications list, select **Work.com**.</span></span>

    ![應用程式清單中的 Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="3a387-277">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3a387-277">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="3a387-279">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a387-279">Click **Add** button.</span></span> <span data-ttu-id="3a387-280">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3a387-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="3a387-282">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="3a387-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3a387-283">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a387-283">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a387-284">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a387-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3a387-285">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3a387-285">Test single sign-on</span></span>

<span data-ttu-id="3a387-286">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="3a387-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3a387-287">當您在「存取面板」中按一下 [Work.com] 圖格時，應該會自動登入您的 Work.com 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a387-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span></span>
<span data-ttu-id="3a387-288">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3a387-288">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a387-289">其他資源</span><span class="sxs-lookup"><span data-stu-id="3a387-289">Additional resources</span></span>

* [<span data-ttu-id="3a387-290">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="3a387-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a387-291">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3a387-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

