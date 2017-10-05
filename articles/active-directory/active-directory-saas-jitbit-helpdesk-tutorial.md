---
title: "教學課程：Azure Active Directory 與 Jitbit Helpdesk 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Jitbit Helpdesk 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 6523ee3179dafd79528093b856b0ec10fafb4f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="84903-103">教學課程：Azure Active Directory 與 Jitbit Helpdesk 整合</span><span class="sxs-lookup"><span data-stu-id="84903-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="84903-104">在本教學課程中，您將了解如何整合 Jitbit Helpdesk 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="84903-104">In this tutorial, you learn how to integrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84903-105">Jitbit Helpdesk 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="84903-105">Integrating Jitbit Helpdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="84903-106">您可以在 Azure AD 中控制可存取 Jitbit Helpdesk 的人員</span><span class="sxs-lookup"><span data-stu-id="84903-106">You can control in Azure AD who has access to Jitbit Helpdesk</span></span>
- <span data-ttu-id="84903-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Jitbit Helpdesk (單一登入)</span><span class="sxs-lookup"><span data-stu-id="84903-107">You can enable your users to automatically get signed-on to Jitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="84903-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="84903-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="84903-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="84903-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84903-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="84903-110">Prerequisites</span></span>

<span data-ttu-id="84903-111">若要設定與 Jitbit Helpdesk 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="84903-111">To configure Azure AD integration with Jitbit Helpdesk, you need the following items:</span></span>

- <span data-ttu-id="84903-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="84903-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84903-113">已啟用 Jitbit Helpdesk 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="84903-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84903-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="84903-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84903-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="84903-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84903-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="84903-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84903-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="84903-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84903-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="84903-118">Scenario description</span></span>
<span data-ttu-id="84903-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84903-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84903-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="84903-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84903-121">從資源庫新增 Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="84903-121">Adding Jitbit Helpdesk from the gallery</span></span>
2. <span data-ttu-id="84903-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84903-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-the-gallery"></a><span data-ttu-id="84903-123">從資源庫新增 Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="84903-123">Adding Jitbit Helpdesk from the gallery</span></span>
<span data-ttu-id="84903-124">若要設定將 Jitbit Helpdesk 整合到 Azure AD 中，您需要從資源庫將 Jitbit Helpdesk 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="84903-124">To configure the integration of Jitbit Helpdesk into Azure AD, you need to add Jitbit Helpdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="84903-125">**若要從資源庫新增 Jitbit Helpdesk，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84903-125">**To add Jitbit Helpdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="84903-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="84903-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="84903-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="84903-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="84903-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="84903-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="84903-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84903-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="84903-133">在搜尋方塊中，輸入 **Jitbit Helpdesk**。</span><span class="sxs-lookup"><span data-stu-id="84903-133">In the search box, type **Jitbit Helpdesk**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="84903-135">在結果窗格中，選取 [Jitbit Helpdesk]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="84903-135">In the results panel, select **Jitbit Helpdesk**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="84903-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84903-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="84903-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Jitbit Helpdesk 設定和測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84903-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84903-139">若要讓單一登入運作，Azure AD 必須知道 Jitbit Helpdesk 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="84903-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jitbit Helpdesk is to a user in Azure AD.</span></span> <span data-ttu-id="84903-140">換句話說，必須建立 Azure AD 使用者和 Jitbit Helpdesk 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="84903-140">In other words, a link relationship between an Azure AD user and the related user in Jitbit Helpdesk needs to be established.</span></span>

<span data-ttu-id="84903-141">在 Jitbit Helpdesk 中，將**使用者名稱**的值指派為 Azure AD 中**使用者名稱**的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="84903-141">In Jitbit Helpdesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="84903-142">若要設定及測試與 Jitbit Helpdesk 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="84903-142">To configure and test Azure AD single sign-on with Jitbit Helpdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="84903-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="84903-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="84903-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84903-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84903-145">**[建立 Jitbit Helpdesk 測試使用者](#creating-a-jitbit-helpdesk-test-user)** - 使 Jitbit Helpdesk 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="84903-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - to have a counterpart of Britta Simon in Jitbit Helpdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="84903-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84903-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84903-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="84903-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="84903-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84903-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="84903-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Jitbit Helpdesk 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="84903-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="84903-150">**若要使用 Jitbit Helpdesk 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84903-150">**To configure Azure AD single sign-on with Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="84903-151">在 Azure 入口網站的 [Jitbit Helpdesk] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="84903-151">In the Azure portal, on the **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="84903-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="84903-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="84903-155">在 [Jitbit Helpdesk 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84903-155">On the **Jitbit Helpdesk Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="84903-157">a.</span><span class="sxs-lookup"><span data-stu-id="84903-157">a.</span></span> <span data-ttu-id="84903-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰</span><span class="sxs-lookup"><span data-stu-id="84903-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="84903-159">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="84903-159">This value is not real.</span></span> <span data-ttu-id="84903-160">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="84903-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="84903-161">請連絡 [Jitbit Helpdesk 用戶端支援小組](https://www.jitbit.com/support/)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="84903-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) to get this value.</span></span> 
    
    <span data-ttu-id="84903-162">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="84903-162">b.</span></span>  <span data-ttu-id="84903-163">在 [識別碼] 文字方塊中輸入如下的 URL：`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="84903-163">In the **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="84903-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="84903-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="84903-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="84903-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="84903-168">在 [Jitbit Helpdesk 設定] 區段中，按一下 [設定 Jitbit Helpdesk] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="84903-168">On the **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="84903-169">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="84903-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="84903-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Jitbit Helpdesk 公司網站。</span><span class="sxs-lookup"><span data-stu-id="84903-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="84903-172">在頂端的工具列中，按一下 [系統管理] 。</span><span class="sxs-lookup"><span data-stu-id="84903-172">In the toolbar on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="84903-173">![管理](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "管理")</span><span class="sxs-lookup"><span data-stu-id="84903-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="84903-174">按一下 [一般設定] 。</span><span class="sxs-lookup"><span data-stu-id="84903-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="84903-175">![使用者、公司和權限](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "使用者、公司和權限")</span><span class="sxs-lookup"><span data-stu-id="84903-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="84903-176">在 [驗證設定]  組態區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84903-176">In the **Authentication settings** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="84903-177">![驗證設定](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "驗證設定")</span><span class="sxs-lookup"><span data-stu-id="84903-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="84903-178">a.</span><span class="sxs-lookup"><span data-stu-id="84903-178">a.</span></span> <span data-ttu-id="84903-179">選取 [啟用 SAML 2.0 單一登入]，以搭配 **OneLogin** 使用單一登入 (SSO) 來登入。</span><span class="sxs-lookup"><span data-stu-id="84903-179">Select **Enable SAML 2.0 single sign on**, to sign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="84903-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="84903-180">b.</span></span> <span data-ttu-id="84903-181">在 [端點 URL] 文字方塊中，貼上您從 Azure 入口網站複製的**「SAML 單一登入服務 URL」**值。</span><span class="sxs-lookup"><span data-stu-id="84903-181">In the **EndPoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="84903-182">c.</span><span class="sxs-lookup"><span data-stu-id="84903-182">c.</span></span> <span data-ttu-id="84903-183">在記事本中開啟您的 **base-64** 編碼的憑證，將它的內容複製到您的剪貼簿，然後貼到 [X.509 憑證] 文字方塊中</span><span class="sxs-lookup"><span data-stu-id="84903-183">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="84903-184">d.</span><span class="sxs-lookup"><span data-stu-id="84903-184">d.</span></span> <span data-ttu-id="84903-185">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="84903-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="84903-186">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="84903-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="84903-187">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="84903-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="84903-188">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84903-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="84903-189">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84903-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="84903-190">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="84903-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="84903-192">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84903-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="84903-193">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="84903-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="84903-195">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="84903-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="84903-197">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="84903-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="84903-199">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84903-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="84903-201">a.</span><span class="sxs-lookup"><span data-stu-id="84903-201">a.</span></span> <span data-ttu-id="84903-202">在 [名稱] 文字方塊中，輸入 **BrittaSimon** 作為名稱。</span><span class="sxs-lookup"><span data-stu-id="84903-202">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="84903-203">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="84903-203">b.</span></span> <span data-ttu-id="84903-204">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="84903-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="84903-205">c.</span><span class="sxs-lookup"><span data-stu-id="84903-205">c.</span></span> <span data-ttu-id="84903-206">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="84903-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="84903-207">d.</span><span class="sxs-lookup"><span data-stu-id="84903-207">d.</span></span> <span data-ttu-id="84903-208">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="84903-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="84903-209">建立 Jitbit Helpdesk 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84903-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="84903-210">為了讓 Azure AD 使用者登入 Jitbit Helpdesk，他們必須佈建到 Jitbit Helpdesk 中。</span><span class="sxs-lookup"><span data-stu-id="84903-210">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="84903-211">在 Jitbit Helpdesk 的情況下，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="84903-211">In the case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="84903-212">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84903-212">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="84903-213">登入您的 **Jitbit Helpdesk** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="84903-213">Log in to your **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="84903-214">在頂端的功能表中，按一下 [系統管理] 。</span><span class="sxs-lookup"><span data-stu-id="84903-214">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="84903-215">![管理](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "管理")</span><span class="sxs-lookup"><span data-stu-id="84903-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="84903-216">按一下 [使用者、公司和權限] 。</span><span class="sxs-lookup"><span data-stu-id="84903-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="84903-217">![使用者、公司和權限](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "使用者、公司和權限")</span><span class="sxs-lookup"><span data-stu-id="84903-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="84903-218">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="84903-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="84903-219">![新增使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="84903-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="84903-220">在 [建立] 區段中，輸入您想要佈建的 Azure AD 帳戶資料，如下所示：</span><span class="sxs-lookup"><span data-stu-id="84903-220">In the Create section, type the data of the Azure AD account you want to provision as follows:</span></span>

    <span data-ttu-id="84903-221">![建立](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "建立")</span><span class="sxs-lookup"><span data-stu-id="84903-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="84903-222">a.</span><span class="sxs-lookup"><span data-stu-id="84903-222">a.</span></span> <span data-ttu-id="84903-223">在 [使用者名稱] 文字方塊中輸入 **BrittaSimon**，亦即 Azure 入口網站中的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="84903-223">In the **Username** textbox, type **BrittaSimon**, the user name as in the Azure portal.</span></span>

   <span data-ttu-id="84903-224">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="84903-224">b.</span></span> <span data-ttu-id="84903-225">在 [電子郵件] 文字方塊中，輸入使用者的電子郵件，例如 **BrittaSimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="84903-225">In the **Email** textbox, type email of the user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="84903-226">c.</span><span class="sxs-lookup"><span data-stu-id="84903-226">c.</span></span> <span data-ttu-id="84903-227">在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="84903-227">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>

   <span data-ttu-id="84903-228">d.</span><span class="sxs-lookup"><span data-stu-id="84903-228">d.</span></span> <span data-ttu-id="84903-229">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="84903-229">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span>
   
   <span data-ttu-id="84903-230">e.</span><span class="sxs-lookup"><span data-stu-id="84903-230">e.</span></span> <span data-ttu-id="84903-231">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="84903-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="84903-232">您可以使用任何其他的 Jitbit Helpdesk 使用者帳戶建立工具或 Jitbit Helpdesk 提供的 API，來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="84903-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="84903-233">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84903-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="84903-234">在本節中，您會將 Jitbit Helpdesk 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84903-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jitbit Helpdesk.</span></span>

![指派使用者][200] 

<span data-ttu-id="84903-236">**若要將 Britta Simon 指派到 Jitbit Helpdesk，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="84903-236">**To assign Britta Simon to Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="84903-237">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="84903-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="84903-239">在應用程式清單中，選取 **Jitbit Helpdesk**。</span><span class="sxs-lookup"><span data-stu-id="84903-239">In the applications list, select **Jitbit Helpdesk**.</span></span>

    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="84903-241">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="84903-241">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="84903-243">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84903-243">Click **Add** button.</span></span> <span data-ttu-id="84903-244">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="84903-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="84903-246">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="84903-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="84903-247">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84903-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84903-248">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84903-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="84903-249">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="84903-249">Testing single sign-on</span></span>

<span data-ttu-id="84903-250">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="84903-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="84903-251">當您按一下存取面板中的 [Jitbit Helpdesk] 圖格時，您應該會看到 Jitbit Helpdesk 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="84903-251">When you click the Jitbit Helpdesk tile in the Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="84903-252">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="84903-252">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84903-253">其他資源</span><span class="sxs-lookup"><span data-stu-id="84903-253">Additional resources</span></span>

* [<span data-ttu-id="84903-254">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="84903-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84903-255">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="84903-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

