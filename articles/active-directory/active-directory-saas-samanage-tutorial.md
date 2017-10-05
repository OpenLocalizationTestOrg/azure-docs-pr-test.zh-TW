---
title: "教學課程：Azure Active Directory 與 Samanage 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Samanage 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c54dbe407145a29a712acc3c0fb549a38ac26bed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="e6c62-103">教學課程：Azure Active Directory 與 Samanage 整合</span><span class="sxs-lookup"><span data-stu-id="e6c62-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="e6c62-104">在本教學課程中，您會了解如何整合 Samanage 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e6c62-104">In this tutorial, you learn how to integrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e6c62-105">Samanage 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="e6c62-105">Integrating Samanage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e6c62-106">您可以在 Azure AD 中控制可存取 Samanage 的人員</span><span class="sxs-lookup"><span data-stu-id="e6c62-106">You can control in Azure AD who has access to Samanage</span></span>
- <span data-ttu-id="e6c62-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Samanage (單一登入)</span><span class="sxs-lookup"><span data-stu-id="e6c62-107">You can enable your users to automatically get signed-on to Samanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e6c62-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="e6c62-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e6c62-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e6c62-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6c62-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e6c62-110">Prerequisites</span></span>

<span data-ttu-id="e6c62-111">若要設定 Azure AD 與 Samanage 的整合作業，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e6c62-111">To configure Azure AD integration with Samanage, you need the following items:</span></span>

- <span data-ttu-id="e6c62-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e6c62-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e6c62-113">啟用 Samanage 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e6c62-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e6c62-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e6c62-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e6c62-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e6c62-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e6c62-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e6c62-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e6c62-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="e6c62-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e6c62-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e6c62-118">Scenario description</span></span>
<span data-ttu-id="e6c62-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6c62-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e6c62-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="e6c62-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e6c62-121">從資源庫新增 Samanage</span><span class="sxs-lookup"><span data-stu-id="e6c62-121">Adding Samanage from the gallery</span></span>
2. <span data-ttu-id="e6c62-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e6c62-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-the-gallery"></a><span data-ttu-id="e6c62-123">從資源庫新增 Samanage</span><span class="sxs-lookup"><span data-stu-id="e6c62-123">Adding Samanage from the gallery</span></span>
<span data-ttu-id="e6c62-124">若要設定 Samanage 與 Azure AD 的整合作業，您必須從資源庫將 Samanage 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="e6c62-124">To configure the integration of Samanage into Azure AD, you need to add Samanage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e6c62-125">**若要從資源庫新增 Samanage，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6c62-125">**To add Samanage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e6c62-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e6c62-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e6c62-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e6c62-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e6c62-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6c62-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e6c62-133">在搜尋方塊中，輸入 **Samanage**。</span><span class="sxs-lookup"><span data-stu-id="e6c62-133">In the search box, type **Samanage**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="e6c62-135">在結果面板中，選取 [Samanage]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6c62-135">In the results panel, select **Samanage**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e6c62-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e6c62-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e6c62-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Samanage 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6c62-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e6c62-139">若要讓單一登入運作，Azure AD 必須知道 Samanage 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="e6c62-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Samanage is to a user in Azure AD.</span></span> <span data-ttu-id="e6c62-140">換句話說，必須在 Azure AD 使用者和 Samanage 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e6c62-140">In other words, a link relationship between an Azure AD user and the related user in Samanage needs to be established.</span></span>

<span data-ttu-id="e6c62-141">在 Samanage 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e6c62-141">In Samanage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e6c62-142">若要使用 Samanage 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e6c62-142">To configure and test Azure AD single sign-on with Samanage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e6c62-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="e6c62-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e6c62-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6c62-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e6c62-145">**[建立 Samanage 測試使用者](#creating-a-samanage-test-user)** - 使 Samanage 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="e6c62-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - to have a counterpart of Britta Simon in Samanage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e6c62-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6c62-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e6c62-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="e6c62-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e6c62-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e6c62-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e6c62-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Samanage 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6c62-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="e6c62-150">**若要使用 Samanage 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6c62-150">**To configure Azure AD single sign-on with Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="e6c62-151">在 Azure 入口網站的 [Samanage] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-151">In the Azure portal, on the **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e6c62-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6c62-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="e6c62-155">在 [Samanage 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e6c62-155">On the **Samanage Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="e6c62-157">a.</span><span class="sxs-lookup"><span data-stu-id="e6c62-157">a.</span></span> <span data-ttu-id="e6c62-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="e6c62-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="e6c62-159">b.</span><span class="sxs-lookup"><span data-stu-id="e6c62-159">b.</span></span> <span data-ttu-id="e6c62-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="e6c62-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e6c62-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="e6c62-161">These values are not real.</span></span> <span data-ttu-id="e6c62-162">請使用實際的「登入 URL」及「識別碼」來更新這些值 (本教學課程稍後會說明)。</span><span class="sxs-lookup"><span data-stu-id="e6c62-162">Update these values with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> <span data-ttu-id="e6c62-163">如需詳細資料，請連絡 [Samanage 客戶支援小組](https://www.samanage.com/support)。</span><span class="sxs-lookup"><span data-stu-id="e6c62-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="e6c62-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e6c62-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="e6c62-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6c62-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e6c62-168">在 [Samanage 組態] 區段上，按一下 [設定 Samanage] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="e6c62-168">On the **Samanage Configuration** section, click **Configure Samanage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e6c62-169">從 [快速參考] 區段中複製 [登出 URL] 和 [SAML 實體識別碼]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="e6c62-171">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Samanage 公司網站。</span><span class="sxs-lookup"><span data-stu-id="e6c62-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="e6c62-172">按一下 [儀表板] 並選取左側導覽窗格中的 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="e6c62-173">![儀表板](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "儀表板")</span><span class="sxs-lookup"><span data-stu-id="e6c62-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="e6c62-174">按一下 [單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="e6c62-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="e6c62-175">![單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="e6c62-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="e6c62-176">瀏覽至 [使用 SAML 登入]  區段，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="e6c62-176">Navigate to **Login using SAML** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e6c62-177">![使用 SAML 登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "使用 SAML 登入")</span><span class="sxs-lookup"><span data-stu-id="e6c62-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="e6c62-178">a.</span><span class="sxs-lookup"><span data-stu-id="e6c62-178">a.</span></span> <span data-ttu-id="e6c62-179">按一下 [使用 SAML 啟用單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="e6c62-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6c62-180">b.</span></span> <span data-ttu-id="e6c62-181">在 [識別提供者 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="e6c62-181">In the **Identity Provider URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="e6c62-182">c.</span><span class="sxs-lookup"><span data-stu-id="e6c62-182">c.</span></span> <span data-ttu-id="e6c62-183">確認 [登入 URL] 符合 Azure 入口網站中 [Samanage 網域及 URL] 區段的 [登入 URL]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-183">Confirm the **Login URL** matches the **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="e6c62-184">d.</span><span class="sxs-lookup"><span data-stu-id="e6c62-184">d.</span></span> <span data-ttu-id="e6c62-185">在 [登出 URL] 文字方塊中，輸入您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="e6c62-185">In the **Logout URL** textbox, enter the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="e6c62-186">e.</span><span class="sxs-lookup"><span data-stu-id="e6c62-186">e.</span></span> <span data-ttu-id="e6c62-187">在 [SAML 簽發者] 文字方塊中，輸入識別提供者中所設定的應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="e6c62-187">In the **SAML Issuer** textbox, type the app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="e6c62-188">f.</span><span class="sxs-lookup"><span data-stu-id="e6c62-188">f.</span></span> <span data-ttu-id="e6c62-189">在記事本中，開啟您從 Azure 入口網站下載的 base-64 編碼憑證，將其內容複製到剪貼簿，然後貼到 [在下面貼上識別提供者 x.509 憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="e6c62-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="e6c62-190">g.</span><span class="sxs-lookup"><span data-stu-id="e6c62-190">g.</span></span> <span data-ttu-id="e6c62-191">按一下 [若 Samanage 中不存在使用者則加以建立]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="e6c62-192">h.</span><span class="sxs-lookup"><span data-stu-id="e6c62-192">h.</span></span> <span data-ttu-id="e6c62-193">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="e6c62-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="e6c62-194">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="e6c62-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e6c62-195">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="e6c62-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e6c62-196">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e6c62-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e6c62-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e6c62-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="e6c62-198">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e6c62-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e6c62-200">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6c62-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e6c62-201">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e6c62-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e6c62-203">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e6c62-205">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e6c62-207">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e6c62-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e6c62-209">a.</span><span class="sxs-lookup"><span data-stu-id="e6c62-209">a.</span></span> <span data-ttu-id="e6c62-210">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e6c62-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e6c62-211">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6c62-211">b.</span></span> <span data-ttu-id="e6c62-212">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="e6c62-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e6c62-213">c.</span><span class="sxs-lookup"><span data-stu-id="e6c62-213">c.</span></span> <span data-ttu-id="e6c62-214">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="e6c62-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e6c62-215">d.</span><span class="sxs-lookup"><span data-stu-id="e6c62-215">d.</span></span> <span data-ttu-id="e6c62-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e6c62-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="e6c62-217">建立 Samanage 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e6c62-217">Creating a Samanage test user</span></span>

<span data-ttu-id="e6c62-218">若要讓 Azure AD 使用者能夠登入 Samanage，必須將他們佈建到 Samanage。</span><span class="sxs-lookup"><span data-stu-id="e6c62-218">To enable Azure AD users to log in to Samanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="e6c62-219">就 Samanage 而言，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="e6c62-219">In the case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="e6c62-220">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6c62-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e6c62-221">以系統管理員身分登入您的 Samanage 公司網站。</span><span class="sxs-lookup"><span data-stu-id="e6c62-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="e6c62-222">按一下 [儀表板] 並選取左側導覽窗格中的 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="e6c62-223">![設定](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "設定")</span><span class="sxs-lookup"><span data-stu-id="e6c62-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="e6c62-224">按一下 [使用者]  索引標籤</span><span class="sxs-lookup"><span data-stu-id="e6c62-224">Click the **Users** tab</span></span>
   
    <span data-ttu-id="e6c62-225">![使用者](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="e6c62-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="e6c62-226">按一下 [新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="e6c62-226">Click **New User**.</span></span>
   
    <span data-ttu-id="e6c62-227">![新增使用者](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="e6c62-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="e6c62-228">輸入您想要佈建之 Azure Active Directory 帳戶的 [名稱] 和 [電子郵件地址]，然後按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-228">Type the **Name** and the **Email Address** of an Azure Active Directory account you want to provision and click **Create user**.</span></span>
   
    <span data-ttu-id="e6c62-229">![建立使用者](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="e6c62-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e6c62-230">Azure Active Directory 帳戶的持有者會收到一封電子郵件，並依照連結在啟用其帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="e6c62-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="e6c62-231">您可以使用任何其他的 Samanage 使用者帳戶建立工具，或 Samanage 提供的 API，以佈建 Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e6c62-231">You can use any other Samanage user account creation tools or APIs provided by Samanage to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e6c62-232">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e6c62-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e6c62-233">在本節中，您會將 Samanage 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6c62-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Samanage.</span></span>

![指派使用者][200] 

<span data-ttu-id="e6c62-235">**若要將 Britta Simon 指派給 Samanage，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6c62-235">**To assign Britta Simon to Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="e6c62-236">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e6c62-238">在應用程式清單中，選取 [Samanage] 。</span><span class="sxs-lookup"><span data-stu-id="e6c62-238">In the applications list, select **Samanage**.</span></span>

    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="e6c62-240">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-240">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e6c62-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6c62-242">Click **Add** button.</span></span> <span data-ttu-id="e6c62-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e6c62-245">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="e6c62-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e6c62-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6c62-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e6c62-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6c62-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e6c62-248">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e6c62-248">Testing single sign-on</span></span>

<span data-ttu-id="e6c62-249">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="e6c62-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e6c62-250">當您在存取面板中按一下 [Samanage] 圖格時，應該會自動登入您的 Samanage 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6c62-250">When you click the Samanage tile in the Access Panel, you should get automatically signed-on to your Samanage application.</span></span>
<span data-ttu-id="e6c62-251">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e6c62-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e6c62-252">其他資源</span><span class="sxs-lookup"><span data-stu-id="e6c62-252">Additional resources</span></span>

* [<span data-ttu-id="e6c62-253">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="e6c62-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e6c62-254">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e6c62-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

