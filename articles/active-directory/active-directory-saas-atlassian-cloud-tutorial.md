---
title: "教學課程：Azure Active Directory 與 Atlassian Cloud 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Atlassian Cloud 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 2891838b56dd15cb5f97dcae391770143a80c781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="21937-103">教學課程：Azure Active Directory 與 Atlassian Cloud 整合</span><span class="sxs-lookup"><span data-stu-id="21937-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="21937-104">在本教學課程中，您會了解如何整合 Atlassian Cloud 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="21937-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="21937-105">Atlassian Cloud 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="21937-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="21937-106">您可以在 Azure AD 中控制可存取 Atlassian Cloud 的人員</span><span class="sxs-lookup"><span data-stu-id="21937-106">You can control in Azure AD who has access to Atlassian Cloud</span></span>
- <span data-ttu-id="21937-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Atlassian Cloud (單一登入)</span><span class="sxs-lookup"><span data-stu-id="21937-107">You can enable your users to automatically get signed-on to Atlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="21937-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="21937-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="21937-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="21937-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21937-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="21937-110">Prerequisites</span></span>

<span data-ttu-id="21937-111">若要設定 Azure AD 與 Atlassian Cloud 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="21937-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span></span>

- <span data-ttu-id="21937-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="21937-112">An Azure AD subscription</span></span>
- <span data-ttu-id="21937-113">已啟用 Atlassian Cloud 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="21937-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="21937-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="21937-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="21937-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="21937-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="21937-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="21937-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="21937-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="21937-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="21937-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="21937-118">Scenario description</span></span>
<span data-ttu-id="21937-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="21937-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="21937-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="21937-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="21937-121">從資源庫新增 Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="21937-121">Adding Atlassian Cloud from the gallery</span></span>
2. <span data-ttu-id="21937-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="21937-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-the-gallery"></a><span data-ttu-id="21937-123">從資源庫新增 Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="21937-123">Adding Atlassian Cloud from the gallery</span></span>
<span data-ttu-id="21937-124">若要設定將 Atlassian Cloud 整合到 Azure AD 中，您需要從資源庫將 Atlassian Cloud 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="21937-124">To configure the integration of Atlassian Cloud into Azure AD, you need to add Atlassian Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="21937-125">**若要從資源庫新增 Atlassian Cloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="21937-125">**To add Atlassian Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="21937-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="21937-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="21937-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="21937-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="21937-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="21937-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="21937-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21937-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="21937-133">在搜尋方塊中，輸入 **Atlassian Cloud**。</span><span class="sxs-lookup"><span data-stu-id="21937-133">In the search box, type **Atlassian Cloud**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="21937-135">在結果面板中，選取 [Atlassian Cloud]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="21937-135">In the results panel, select **Atlassian Cloud**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="21937-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="21937-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="21937-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Atlassian Cloud 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="21937-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="21937-139">若要讓單一登入能夠運作，Azure AD 必須知道 Atlassian Cloud 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="21937-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atlassian Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="21937-140">換句話說，必須在 Azure AD 使用者與 Atlassian Cloud 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="21937-140">In other words, a link relationship between an Azure AD user and the related user in Atlassian Cloud needs to be established.</span></span>

<span data-ttu-id="21937-141">建立此連結關聯性的方法是將 Azure AD 中**使用者名稱**的值指定為 Atlassian Cloud 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="21937-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="21937-142">若要設定及測試與 Atlassian Cloud 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="21937-142">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="21937-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="21937-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="21937-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="21937-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="21937-145">**[建立 Atlassian Cloud 測試使用者](#creating-an-atlassian-cloud-test-user)** - 在 Atlassian Cloud 中建立一個與 Azure AD 中代表使用者的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="21937-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - to have a counterpart of Britta Simon in Atlassian Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="21937-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="21937-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="21937-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="21937-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="21937-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="21937-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="21937-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Atlassian Cloud 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="21937-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="21937-150">**若要使用 Atlassian Cloud 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="21937-150">**To configure Azure AD single sign-on with Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="21937-151">在 Azure 入口網站的 [Atlassian Cloud] 應用程式整合分頁上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="21937-151">In the Azure portal, on the **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="21937-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="21937-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="21937-155">如果您想要以 **IDP** 起始模式設定應用程式，請在 [Atlassian Cloud 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="21937-155">On the **Atlassian Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="21937-157">a.</span><span class="sxs-lookup"><span data-stu-id="21937-157">a.</span></span> <span data-ttu-id="21937-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="21937-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="21937-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="21937-159">b.</span></span> <span data-ttu-id="21937-160">在 [回覆 URL] 文字方塊中，輸入 URL 為：`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="21937-160">In the **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="21937-161">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="21937-161">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="21937-163">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="21937-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="21937-164">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="21937-164">These values are not real.</span></span> <span data-ttu-id="21937-165">請使用實際的識別碼和登入 URL 將這些值更新。</span><span class="sxs-lookup"><span data-stu-id="21937-165">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="21937-166">您可以從 [Atlassian Cloud SAML 設定] 畫面取得確切值。</span><span class="sxs-lookup"><span data-stu-id="21937-166">You can get the exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="21937-167">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="21937-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="21937-169">在 [Atlassian Cloud 設定] 區段中，按一下 [設定 Atlassian Cloud] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="21937-169">On the **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="21937-170">從 [快速參考] 區段中複製 [SAML 實體 ID 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="21937-170">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="21937-172">若要取得針對您的應用程式設定的 SSO，請使用系統管理員權限登入 Atlassian 入口網站。</span><span class="sxs-lookup"><span data-stu-id="21937-172">To get SSO configured for your application, login to the Atlassian Portal using the administrator rights.</span></span>

8. <span data-ttu-id="21937-173">在左側導覽列的 [驗證] 區段中按一下 [網域]。</span><span class="sxs-lookup"><span data-stu-id="21937-173">In the Authentication section of the left navigation click **Domains**.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="21937-175">a.</span><span class="sxs-lookup"><span data-stu-id="21937-175">a.</span></span> <span data-ttu-id="21937-176">在文字方塊中，輸入您的網域名稱，然後按一下 [新增網域]。</span><span class="sxs-lookup"><span data-stu-id="21937-176">In the textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="21937-178">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="21937-178">b.</span></span> <span data-ttu-id="21937-179">若要驗證網域，請按一下 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="21937-179">To verify the domain, click **Verify**.</span></span> 

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="21937-181">c.</span><span class="sxs-lookup"><span data-stu-id="21937-181">c.</span></span> <span data-ttu-id="21937-182">下載網域驗證 html 檔案，將它上傳至您的網域網站的根資料夾，然後按一下 [驗證網域]。</span><span class="sxs-lookup"><span data-stu-id="21937-182">Download the domain verification html file, upload it to the root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="21937-184">d.</span><span class="sxs-lookup"><span data-stu-id="21937-184">d.</span></span> <span data-ttu-id="21937-185">驗證網域後，[狀態] 欄位的值會是 [已驗證]。</span><span class="sxs-lookup"><span data-stu-id="21937-185">Once the domain is verified, the value of the **Status** field is **Verified**.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="21937-187">在左側瀏覽列中，按一下 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="21937-187">In the left navigation bar, click **SAML**.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="21937-189">建立 SAML 設定並新增識別提供者設定。</span><span class="sxs-lookup"><span data-stu-id="21937-189">Create a SAML Configuration and add the Identity provider configuration.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="21937-191">a.</span><span class="sxs-lookup"><span data-stu-id="21937-191">a.</span></span> <span data-ttu-id="21937-192">在 [識別提供者實體識別碼] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="21937-192">In the **Identity provider Entity ID** text box, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="21937-193">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="21937-193">b.</span></span> <span data-ttu-id="21937-194">在 [識別提供者 SSO URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="21937-194">In the **Identity provider SSO URL** text box, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="21937-195">c.</span><span class="sxs-lookup"><span data-stu-id="21937-195">c.</span></span> <span data-ttu-id="21937-196">開啟從 Azure 入口網站下載的憑證，複製不含開始和結束行的值，並將它貼在 [公用 X509 憑證] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="21937-196">Open the downloaded certificate from Azure portal and copy the values without the Begin and End lines and paste it in the **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="21937-197">d.</span><span class="sxs-lookup"><span data-stu-id="21937-197">d.</span></span> <span data-ttu-id="21937-198">按一下 [儲存設定] 以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="21937-198">Click **Save Configuration**  to Save the settings.</span></span>
     
11. <span data-ttu-id="21937-199">更新 Azure AD 設定，確定您已設定正確的識別項 URL。</span><span class="sxs-lookup"><span data-stu-id="21937-199">Update the Azure AD settings to make sure that you have setup the correct Identifier URL.</span></span>
  
    <span data-ttu-id="21937-200">a.</span><span class="sxs-lookup"><span data-stu-id="21937-200">a.</span></span> <span data-ttu-id="21937-201">從 [SAML] 畫面複製 [SP身分識別碼]，然後將它貼在 Azure AD 中作為 [識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="21937-201">Copy the **SP Identity ID** from the SAML screen and paste it in Azure AD as the **Identifier** value.</span></span>

    <span data-ttu-id="21937-202">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="21937-202">b.</span></span> <span data-ttu-id="21937-203">[登入 URL] 是 Atlassian Cloud 的租用戶 URL。</span><span class="sxs-lookup"><span data-stu-id="21937-203">Sign On URL is the tenant URL of your Atlassian Cloud.</span></span>   

     ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="21937-205">在 Azure 入口網站中，按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21937-205">In the Azure portal, Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="21937-207">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="21937-207">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="21937-208">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="21937-208">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="21937-209">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="21937-209">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="21937-210">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="21937-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="21937-211">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="21937-211">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="21937-213">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="21937-213">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="21937-214">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="21937-214">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="21937-216">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="21937-216">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="21937-218">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="21937-218">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="21937-220">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="21937-220">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="21937-222">a.</span><span class="sxs-lookup"><span data-stu-id="21937-222">a.</span></span> <span data-ttu-id="21937-223">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="21937-223">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="21937-224">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="21937-224">b.</span></span> <span data-ttu-id="21937-225">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="21937-225">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="21937-226">c.</span><span class="sxs-lookup"><span data-stu-id="21937-226">c.</span></span> <span data-ttu-id="21937-227">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="21937-227">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="21937-228">d.</span><span class="sxs-lookup"><span data-stu-id="21937-228">d.</span></span> <span data-ttu-id="21937-229">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="21937-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="21937-230">建立 Atlassian Cloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="21937-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="21937-231">若要讓 Azure AD 使用者能夠登入 Atlassian Cloud，必須將他們佈建到 Atlassian Cloud。</span><span class="sxs-lookup"><span data-stu-id="21937-231">To enable Azure AD users to log in to Atlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="21937-232">Atlassian Cloud 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="21937-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="21937-233">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="21937-233">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="21937-234">在 [網站管理] 區段中，按一下 [使用者] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21937-234">In the Site administration section, click the **Users** button</span></span>

    ![建立 Atlassian Cloud 使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="21937-236">按一下 [建立使用者] 按鈕，以在 Atlassian Cloud 中建立使用者。</span><span class="sxs-lookup"><span data-stu-id="21937-236">Click the **Create User** button to create a user in the Atlassian Cloud</span></span>

    ![建立 Atlassian Cloud 使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="21937-238">輸入使用者的 [電子郵件地址]、[使用者名稱] 和 [完整名稱]，然後指派應用程式存取權。</span><span class="sxs-lookup"><span data-stu-id="21937-238">Enter the user's **Email address**, **Username**, and **Full Name** and assign the application access.</span></span> 

    ![建立 Atlassian Cloud 使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="21937-240">按一下 [建立使用者] 按鈕，便會傳送電子郵件邀請給使用者，而使用者在接受邀請之後便可在系統中作業。</span><span class="sxs-lookup"><span data-stu-id="21937-240">Click **Create user** button, it will send the email invitation to the user and after accepting the invitation the user will be active in the system.</span></span> 

>[!NOTE] 
><span data-ttu-id="21937-241">您也可以按一下 [使用者] 區段中的 [大量建立] 按鈕，建立大量使用者。</span><span class="sxs-lookup"><span data-stu-id="21937-241">You can also create the bulk users by clicking the **Bulk Create** button in the Users section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="21937-242">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="21937-242">Assigning the Azure AD test user</span></span>

<span data-ttu-id="21937-243">在本節中，您會將 Atlassian Cloud 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="21937-243">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atlassian Cloud.</span></span>

![指派使用者][200] 

<span data-ttu-id="21937-245">**若要將 Britta Simon 指派給 Atlassian Cloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="21937-245">**To assign Britta Simon to Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="21937-246">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="21937-246">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="21937-248">在應用程式清單中，選取 [Atlassian Cloud]。</span><span class="sxs-lookup"><span data-stu-id="21937-248">In the applications list, select **Atlassian Cloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="21937-250">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="21937-250">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="21937-252">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21937-252">Click **Add** button.</span></span> <span data-ttu-id="21937-253">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="21937-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="21937-255">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="21937-255">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="21937-256">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21937-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="21937-257">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21937-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="21937-258">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="21937-258">Testing single sign-on</span></span>

<span data-ttu-id="21937-259">在本節中，您會使用存取面板來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="21937-259">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="21937-260">在存取面板中按一下 [Atlassian Cloud] 圖格時，您應該會自動登入您的 Atlassian Cloud 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21937-260">When you click the Atlassian Cloud tile in the Access Panel, you should get automatically signed-on to your Atlassian Cloud application.</span></span> <span data-ttu-id="21937-261">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="21937-261">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="21937-262">其他資源</span><span class="sxs-lookup"><span data-stu-id="21937-262">Additional resources</span></span>

* [<span data-ttu-id="21937-263">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="21937-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="21937-264">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="21937-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

