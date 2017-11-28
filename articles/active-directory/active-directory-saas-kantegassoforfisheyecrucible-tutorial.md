---
title: "教學課程：Azure Active Directory 與 Kantega SSO for FishEye/Crucible 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Kantega SSO for FishEye/Crucible 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9eaa2ec661a3488b0bef1f6b7cc7a82290720054
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a><span data-ttu-id="de293-103">教學課程：Azure Active Directory 與 Kantega SSO for FishEye/Crucible 整合</span><span class="sxs-lookup"><span data-stu-id="de293-103">Tutorial: Azure Active Directory integration with Kantega SSO for FishEye/Crucible</span></span>

<span data-ttu-id="de293-104">在本教學課程中，您會了解如何整合 Kantega SSO for FishEye/Crucible 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="de293-104">In this tutorial, you learn how to integrate Kantega SSO for FishEye/Crucible with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de293-105">Kantega SSO for FishEye/Crucible 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="de293-105">Integrating Kantega SSO for FishEye/Crucible with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="de293-106">您可以在 Azure AD 中控制可存取 Kantega SSO for FishEye/Crucible 的人員</span><span class="sxs-lookup"><span data-stu-id="de293-106">You can control in Azure AD who has access to Kantega SSO for FishEye/Crucible</span></span>
- <span data-ttu-id="de293-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Kantega SSO for FishEye/Crucible (單一登入)</span><span class="sxs-lookup"><span data-stu-id="de293-107">You can enable your users to automatically get signed-on to Kantega SSO for FishEye/Crucible (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de293-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="de293-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="de293-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="de293-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de293-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="de293-110">Prerequisites</span></span>

<span data-ttu-id="de293-111">若要設定 Azure AD 與 Kantega SSO for FishEye/Crucible 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="de293-111">To configure Azure AD integration with Kantega SSO for FishEye/Crucible, you need the following items:</span></span>

- <span data-ttu-id="de293-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="de293-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de293-113">啟用 Kantega SSO for FishEye/Crucible 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="de293-113">A Kantega SSO for FishEye/Crucible single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de293-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="de293-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de293-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="de293-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de293-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="de293-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de293-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="de293-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de293-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="de293-118">Scenario description</span></span>
<span data-ttu-id="de293-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de293-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de293-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="de293-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de293-121">從資源庫新增 Kantega SSO for FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="de293-121">Adding Kantega SSO for FishEye/Crucible from the gallery</span></span>
2. <span data-ttu-id="de293-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de293-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-fisheyecrucible-from-the-gallery"></a><span data-ttu-id="de293-123">從資源庫新增 Kantega SSO for FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="de293-123">Adding Kantega SSO for FishEye/Crucible from the gallery</span></span>
<span data-ttu-id="de293-124">若要設定將 Kantega SSO for FishEye/Crucible 整合到 Azure AD 中，您需要從資源庫將 Kantega SSO for FishEye/Crucible 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="de293-124">To configure the integration of Kantega SSO for FishEye/Crucible into Azure AD, you need to add Kantega SSO for FishEye/Crucible from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="de293-125">**若要從資源庫新增 Kantega SSO for FishEye/Crucible，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="de293-125">**To add Kantega SSO for FishEye/Crucible from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="de293-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="de293-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de293-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="de293-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="de293-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="de293-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="de293-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de293-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="de293-133">在搜尋方塊中，輸入 **Kantega SSO for FishEye/Crucible**。</span><span class="sxs-lookup"><span data-stu-id="de293-133">In the search box, type **Kantega SSO for FishEye/Crucible**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. <span data-ttu-id="de293-135">在結果面板中，選取 [Kantega SSO for FishEye/Crucible]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="de293-135">In the results panel, select **Kantega SSO for FishEye/Crucible**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de293-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de293-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de293-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Kantega SSO for FishEye/Crucible 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de293-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de293-139">若要讓單一登入運作，Azure AD 必須知道 Kantega SSO for FishEye/Crucible 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="de293-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for FishEye/Crucible is to a user in Azure AD.</span></span> <span data-ttu-id="de293-140">換句話說，必須在 Azure AD 使用者和 Kantega SSO for FishEye/Crucible 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="de293-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for FishEye/Crucible needs to be established.</span></span>

<span data-ttu-id="de293-141">在 Kantega SSO for FishEye/Crucible 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="de293-141">In Kantega SSO for FishEye/Crucible, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="de293-142">若要設定及測試與 Kantega SSO for FishEye/Crucible 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="de293-142">To configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="de293-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="de293-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="de293-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de293-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de293-145">**[建立 Kantega SSO for FishEye/Crucible 測試使用者](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** - 使 Kantega SSO for FishEye/Crucible 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="de293-145">**[Creating a Kantega SSO for FishEye/Crucible test user](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for FishEye/Crucible that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="de293-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de293-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de293-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="de293-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de293-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de293-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de293-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Kantega SSO for FishEye/Crucible 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="de293-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for FishEye/Crucible application.</span></span>

<span data-ttu-id="de293-150">**若要設定與 Kantega SSO for FishEye/Crucible 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="de293-150">**To configure Azure AD single sign-on with Kantega SSO for FishEye/Crucible, perform the following steps:**</span></span>

1. <span data-ttu-id="de293-151">在 Azure 入口網站的 [Kantega SSO for FishEye/Crucible] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="de293-151">In the Azure portal, on the **Kantega SSO for FishEye/Crucible** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="de293-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="de293-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. <span data-ttu-id="de293-155">在 **IDP** 起始模式下，在 [Kantega SSO for FishEye/Crucible 網域及 URL] 區段中執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de293-155">In **IDP** initiated mode, on the **Kantega SSO for FishEye/Crucible Domain and URLs** section perform the following step :</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    <span data-ttu-id="de293-157">a.</span><span class="sxs-lookup"><span data-stu-id="de293-157">a.</span></span> <span data-ttu-id="de293-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="de293-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="de293-159">b.</span><span class="sxs-lookup"><span data-stu-id="de293-159">b.</span></span> <span data-ttu-id="de293-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="de293-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="de293-161">在 **SP** 起始模式下，勾選 [顯示進階 URL 設定]，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de293-161">In **SP** initiated mode, check **Show advanced URL settings** and perform the following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    <span data-ttu-id="de293-163">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="de293-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="de293-164">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="de293-164">These values are not real.</span></span> <span data-ttu-id="de293-165">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="de293-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="de293-166">在設定 FishEye/Crucible 外掛程式 (本教學課程稍後會說明) 期間會收到這些值。</span><span class="sxs-lookup"><span data-stu-id="de293-166">These values are recieved during the configuration of FishEye/Crucible plugin which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="de293-167">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="de293-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. <span data-ttu-id="de293-169">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="de293-169">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="de293-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 FishEye/Crucible 內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="de293-171">In a different web browser window, log in to your FishEye/Crucible on premise server as an administrator.</span></span>

8. <span data-ttu-id="de293-172">將滑鼠停留在 cog 上，然後按一下 [附加元件]。</span><span class="sxs-lookup"><span data-stu-id="de293-172">Hover on cog and click the **Add-ons**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. <span data-ttu-id="de293-174">在 [系統設定] 區段下，按一下 [尋找新的附加元件]。</span><span class="sxs-lookup"><span data-stu-id="de293-174">Under System Settings section, click **Find new add-ons**.</span></span> 

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. <span data-ttu-id="de293-176">搜尋 **Kantega SSO for Crucible**，然後按一下 [安裝] 按鈕以安裝新的 SAML 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="de293-176">Search **Kantega SSO for Crucible** and click **Install** button to install the new SAML plugin.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. <span data-ttu-id="de293-178">外掛程式會開始安裝。</span><span class="sxs-lookup"><span data-stu-id="de293-178">The plugin installation starts.</span></span> 

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. <span data-ttu-id="de293-180">當安裝完成時。</span><span class="sxs-lookup"><span data-stu-id="de293-180">Once the installation is complete.</span></span> <span data-ttu-id="de293-181">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="de293-181">Click **Close**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. <span data-ttu-id="de293-183">按一下 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="de293-183">Click **Manage**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. <span data-ttu-id="de293-185">按一下 [設定] 來設定新的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="de293-185">Click **Configure** to configure the new plugin.</span></span>    

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. <span data-ttu-id="de293-187">在 [SAML] 區段中。</span><span class="sxs-lookup"><span data-stu-id="de293-187">In the **SAML** section.</span></span> <span data-ttu-id="de293-188">從 [新增識別提供者] 下拉式清單中，選取 [Azure Active Directory]\(Azure AD\)。</span><span class="sxs-lookup"><span data-stu-id="de293-188">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. <span data-ttu-id="de293-190">選取 [基本] 作為訂用帳戶層級。</span><span class="sxs-lookup"><span data-stu-id="de293-190">Select subscription level as **Basic**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. <span data-ttu-id="de293-192">在 [應用程式屬性] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de293-192">On the **App properties** section, perform following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    <span data-ttu-id="de293-194">a.</span><span class="sxs-lookup"><span data-stu-id="de293-194">a.</span></span> <span data-ttu-id="de293-195">複製 [應用程式識別碼 URI] 值，然後在 Azure 入口網站的 [Kantega SSO for FishEye/Crucible 網域及 URL] 區段上，使用此 URI 作為 [識別碼]、[回覆 URL] 和 [登入 URL]。</span><span class="sxs-lookup"><span data-stu-id="de293-195">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for FishEye/Crucible Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="de293-196">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="de293-196">b.</span></span> <span data-ttu-id="de293-197">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="de293-197">Click **Next**.</span></span>

18. <span data-ttu-id="de293-198">在 [中繼資料匯入] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de293-198">On the **Metadata import** section, perform following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    <span data-ttu-id="de293-200">a.</span><span class="sxs-lookup"><span data-stu-id="de293-200">a.</span></span> <span data-ttu-id="de293-201">選取 [我的電腦上的中繼資料檔案]，上傳您從 Azure 入口網站下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="de293-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="de293-202">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="de293-202">b.</span></span> <span data-ttu-id="de293-203">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="de293-203">Click **Next**.</span></span>

19. <span data-ttu-id="de293-204">在 [名稱和 SSO 位置] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de293-204">On the **Name and SSO location** section, perform following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    <span data-ttu-id="de293-206">a.</span><span class="sxs-lookup"><span data-stu-id="de293-206">a.</span></span> <span data-ttu-id="de293-207">在 [識別提供者名稱] 文字方塊中，新增識別提供者的名稱 (例如 Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="de293-207">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="de293-208">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="de293-208">b.</span></span> <span data-ttu-id="de293-209">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="de293-209">Click **Next**.</span></span>

20. <span data-ttu-id="de293-210">確認簽署憑證，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="de293-210">Verify the Signing certificate and click **Next**.</span></span>  

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. <span data-ttu-id="de293-212">在 [FishEye 使用者帳戶] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de293-212">On the **FishEye user accounts** section, perform following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    <span data-ttu-id="de293-214">a.</span><span class="sxs-lookup"><span data-stu-id="de293-214">a.</span></span> <span data-ttu-id="de293-215">選取 [如果需要，在 FishEye 的內部目錄中建立使用者]，然後輸入使用者群組的適當名稱 (可以是多個</span><span class="sxs-lookup"><span data-stu-id="de293-215">Select **Create users in FishEye's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="de293-216">群組，以逗號分隔)。</span><span class="sxs-lookup"><span data-stu-id="de293-216">of groups separated by comma).</span></span>

    <span data-ttu-id="de293-217">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="de293-217">b.</span></span> <span data-ttu-id="de293-218">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="de293-218">Click **Next**.</span></span>

22. <span data-ttu-id="de293-219">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="de293-219">Click **Finish**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. <span data-ttu-id="de293-221">在 [Azure AD 的已知網域] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de293-221">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    <span data-ttu-id="de293-223">a.</span><span class="sxs-lookup"><span data-stu-id="de293-223">a.</span></span> <span data-ttu-id="de293-224">從頁面的左面板中，選取 [已知網域]。</span><span class="sxs-lookup"><span data-stu-id="de293-224">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="de293-225">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="de293-225">b.</span></span> <span data-ttu-id="de293-226">在 [已知網域] 文字方塊中，輸入網域名稱。</span><span class="sxs-lookup"><span data-stu-id="de293-226">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="de293-227">c.</span><span class="sxs-lookup"><span data-stu-id="de293-227">c.</span></span> <span data-ttu-id="de293-228">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="de293-228">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="de293-229">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="de293-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="de293-230">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="de293-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="de293-231">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de293-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de293-232">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de293-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="de293-233">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="de293-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="de293-235">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="de293-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="de293-236">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="de293-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de293-238">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="de293-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de293-240">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="de293-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de293-242">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de293-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de293-244">a.</span><span class="sxs-lookup"><span data-stu-id="de293-244">a.</span></span> <span data-ttu-id="de293-245">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="de293-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de293-246">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="de293-246">b.</span></span> <span data-ttu-id="de293-247">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="de293-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de293-248">c.</span><span class="sxs-lookup"><span data-stu-id="de293-248">c.</span></span> <span data-ttu-id="de293-249">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="de293-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="de293-250">d.</span><span class="sxs-lookup"><span data-stu-id="de293-250">d.</span></span> <span data-ttu-id="de293-251">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="de293-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a><span data-ttu-id="de293-252">建立 Kantega SSO for FishEye/Crucible 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de293-252">Creating a Kantega SSO for FishEye/Crucible test user</span></span>

<span data-ttu-id="de293-253">若要讓 Azure AD 使用者能夠登入 FishEye/Crucible，必須將他們佈建到 FishEye/Crucible。</span><span class="sxs-lookup"><span data-stu-id="de293-253">To enable Azure AD users to log in to FishEye/Crucible, they must be provisioned into FishEye/Crucible.</span></span> <span data-ttu-id="de293-254">在 Kantega SSO for FishEye/Crucible 中，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="de293-254">In Kantega SSO for FishEye/Crucible, provisioning is a manual task.</span></span>

<span data-ttu-id="de293-255">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="de293-255">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="de293-256">以系統管理員身分登入您的 Crucible 內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="de293-256">Log in to your Crucible on premise server as an administrator.</span></span>

2. <span data-ttu-id="de293-257">將滑鼠停留在齒輪上，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="de293-257">Hover on cog and click the **Users**.</span></span>

    ![新增員工](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. <span data-ttu-id="de293-259">在 [使用者] 索引標籤區段下，按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="de293-259">Under **Users** tab section, click **Add user**.</span></span>

    ![新增員工](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. <span data-ttu-id="de293-261">在 [新增使用者] 對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de293-261">On the **Add New User** dialog page, perform the following steps:</span></span>

    ![新增員工](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    <span data-ttu-id="de293-263">a.</span><span class="sxs-lookup"><span data-stu-id="de293-263">a.</span></span> <span data-ttu-id="de293-264">在 [使用者名稱] 文字方塊中，輸入像是 Brittasimon@contoso.com 的使用者電子郵件。</span><span class="sxs-lookup"><span data-stu-id="de293-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="de293-265">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="de293-265">b.</span></span> <span data-ttu-id="de293-266">在 [顯示名稱] 文字方塊中，輸入使用者的顯示名稱，例如 Britta Simon。</span><span class="sxs-lookup"><span data-stu-id="de293-266">In the **Display Name** textbox, type display name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="de293-267">c.</span><span class="sxs-lookup"><span data-stu-id="de293-267">c.</span></span> <span data-ttu-id="de293-268">在 [電子郵件地址] 文字方塊中，輸入像是 Brittasimon@contoso.com 的使用者電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="de293-268">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="de293-269">d.</span><span class="sxs-lookup"><span data-stu-id="de293-269">d.</span></span> <span data-ttu-id="de293-270">在 [密碼] 文字方塊中，輸入使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="de293-270">In the **Password** textbox, type the password of user.</span></span>  

    <span data-ttu-id="de293-271">e.</span><span class="sxs-lookup"><span data-stu-id="de293-271">e.</span></span> <span data-ttu-id="de293-272">在 [確認密碼] 文字方塊中，再次輸入使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="de293-272">In the **Confirm Password** textbox, reenter the password of user.</span></span>

    <span data-ttu-id="de293-273">f.</span><span class="sxs-lookup"><span data-stu-id="de293-273">f.</span></span> <span data-ttu-id="de293-274">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="de293-274">Click **Add**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="de293-275">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de293-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="de293-276">在本節中，您會將 Kantega SSO for FishEye/Crucible 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de293-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for FishEye/Crucible.</span></span>

![指派使用者][200] 

<span data-ttu-id="de293-278">**若要將 Britta Simon 指派給 Kantega SSO for FishEye/Crucible，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="de293-278">**To assign Britta Simon to Kantega SSO for FishEye/Crucible, perform the following steps:**</span></span>

1. <span data-ttu-id="de293-279">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="de293-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="de293-281">在應用程式清單中，選取 [Kantega SSO for FishEye/Crucible]。</span><span class="sxs-lookup"><span data-stu-id="de293-281">In the applications list, select **Kantega SSO for FishEye/Crucible**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. <span data-ttu-id="de293-283">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="de293-283">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="de293-285">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de293-285">Click **Add** button.</span></span> <span data-ttu-id="de293-286">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="de293-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="de293-288">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="de293-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="de293-289">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de293-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de293-290">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de293-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de293-291">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="de293-291">Testing single sign-on</span></span>

<span data-ttu-id="de293-292">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="de293-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="de293-293">當您在存取面板中按一下 Kantega SSO for FishEye/Crucible 圖格時，應該會自動登入您的 Kantega SSO for FishEye/Crucible 應用程式。</span><span class="sxs-lookup"><span data-stu-id="de293-293">When you click the Kantega SSO for FishEye/Crucible tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for FishEye/Crucible application.</span></span>
<span data-ttu-id="de293-294">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="de293-294">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="de293-295">其他資源</span><span class="sxs-lookup"><span data-stu-id="de293-295">Additional resources</span></span>

* [<span data-ttu-id="de293-296">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="de293-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de293-297">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="de293-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png

