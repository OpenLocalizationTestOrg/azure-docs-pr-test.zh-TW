---
title: "教學課程：Azure Active Directory 與 PlanMyLeave | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 PlanMyLeave 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: ba418a641b339a0d94a3c7b2596d37fbd88a30c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="2f7d2-103">教學課程：Azure Active Directory 與 PlanMyLeave 整合</span><span class="sxs-lookup"><span data-stu-id="2f7d2-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="2f7d2-104">在本教學課程中，您會了解如何整合 PlanMyLeave 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f7d2-105">PlanMyLeave 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="2f7d2-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2f7d2-106">您可以在 Azure AD 中控制可存取 PlanMyLeave 的人員</span><span class="sxs-lookup"><span data-stu-id="2f7d2-106">You can control in Azure AD who has access to PlanMyLeave</span></span>
- <span data-ttu-id="2f7d2-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 PlanMyLeave (單一登入)</span><span class="sxs-lookup"><span data-stu-id="2f7d2-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f7d2-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="2f7d2-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2f7d2-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f7d2-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="2f7d2-110">Prerequisites</span></span>

<span data-ttu-id="2f7d2-111">若要設定與 PlanMyLeave 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="2f7d2-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span></span>

- <span data-ttu-id="2f7d2-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2f7d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f7d2-113">啟用 PlanMyLeave 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2f7d2-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="2f7d2-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="2f7d2-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="2f7d2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f7d2-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2f7d2-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="2f7d2-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="2f7d2-118">Scenario description</span></span>
<span data-ttu-id="2f7d2-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f7d2-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="2f7d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f7d2-121">從資源庫中新增 PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="2f7d2-121">Adding PlanMyLeave from the gallery</span></span>
2. <span data-ttu-id="2f7d2-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2f7d2-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-the-gallery"></a><span data-ttu-id="2f7d2-123">從資源庫中新增 PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="2f7d2-123">Adding PlanMyLeave from the gallery</span></span>
<span data-ttu-id="2f7d2-124">若要設定 PlanMyLeave 與 Azure AD 整合，您需要從資源庫將 PlanMyLeave 加入到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f7d2-125">**若要從資源庫新增 PlanMyLeave，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="2f7d2-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2f7d2-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f7d2-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2f7d2-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="2f7d2-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="2f7d2-133">在搜尋方塊中，輸入 **PlanMyLeave**。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-133">In the search box, type **PlanMyLeave**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="2f7d2-135">在結果窗格中，選取 [PlanMyLeave]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f7d2-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2f7d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f7d2-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 PlanMyLeave 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f7d2-139">若要讓單一登入運作，Azure AD 必須知道 PlanMyLeave 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span></span> <span data-ttu-id="2f7d2-140">換句話說，必須在 Azure AD 使用者和 PlanMyLeave 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span></span>

<span data-ttu-id="2f7d2-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 PlanMyLeave 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="2f7d2-142">若要使用 PlanMyLeave 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="2f7d2-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2f7d2-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2f7d2-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f7d2-145">**[建立 PlanMyLeave 測試使用者](#creating-a-planmyleave-test-user)** - 使 PlanMyLeave 中 Britta Simon 的對應使用者連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2f7d2-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f7d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f7d2-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2f7d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f7d2-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 PlanMyLeave 中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="2f7d2-150">**若要使用 PlanMyLeave 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="2f7d2-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="2f7d2-151">在 Azure 管理入口網站的 [PlanMyLeave] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="2f7d2-153">在 [單一登入] 對話方塊頁面上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="2f7d2-155">在 [PlanMyLeave 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2f7d2-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="2f7d2-157">a.</span><span class="sxs-lookup"><span data-stu-id="2f7d2-157">a.</span></span> <span data-ttu-id="2f7d2-158">在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="2f7d2-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="2f7d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="2f7d2-159">b.</span></span> <span data-ttu-id="2f7d2-160">在 [識別碼] 文字方塊中，以下列模式輸入 URL：`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="2f7d2-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2f7d2-161">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-161">Please note that these are not the real values.</span></span> <span data-ttu-id="2f7d2-162">您必須使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="2f7d2-163">請連絡 [PlanMyLeave 支援小組](mailto:support@planmyleave.com)，以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span></span>

4. <span data-ttu-id="2f7d2-164">在 [SAML 簽署憑證] 區段中，按一下 [建立新憑證]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="2f7d2-166">在 [建立新憑證] 對話方塊中，按一下行事曆圖示並選取 [到期日]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="2f7d2-167">然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-167">Then click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="2f7d2-169">在 [SAML 簽署憑證] 區段中，選取 [啟用新憑證] 並按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="2f7d2-171">在 [變換憑證] 快顯視窗上，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2f7d2-173">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="2f7d2-175">在 [PlanMyLeave 組態] 區段上，按一下 [設定 PlanMyLeave] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="2f7d2-178">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 PlanMyLeave 租用戶。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="2f7d2-179">移至 [系統設定]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-179">Go to **System Setup**.</span></span> <span data-ttu-id="2f7d2-180">接著，在 [安全性管理] 區段上，按一下 [公司 SAML 設定]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-180">Then on the **Security Management** section click **Company SAML settings** .</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="2f7d2-182">在 [SAML 設定] 區段上，按一下編輯器圖示。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-182">On the **SAML Settings** section, click editor icon.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="2f7d2-184">在 [更新 SAML 設定] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2f7d2-184">On the **Update SAML Settings** section, perform the following steps:</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="2f7d2-186">a.</span><span class="sxs-lookup"><span data-stu-id="2f7d2-186">a.</span></span>  <span data-ttu-id="2f7d2-187">在 [登入 URL] 文字方塊中，放入來自 Azure AD 應用程式組態視窗的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="2f7d2-188">b.</span><span class="sxs-lookup"><span data-stu-id="2f7d2-188">b.</span></span>  <span data-ttu-id="2f7d2-189">在記事本中開啟您下載的憑證檔，只將 ---Begin Certificate--- 和 ---End Certificate---- 之間的內容複製到剪貼簿上，然後貼到 [憑證]  文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>

    <span data-ttu-id="2f7d2-190">c.</span><span class="sxs-lookup"><span data-stu-id="2f7d2-190">c.</span></span> <span data-ttu-id="2f7d2-191">將 "**Is Enable**" 設定為 "**Yes**"。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-191">Set "**Is Enable**" to "**Yes**".</span></span>

    <span data-ttu-id="2f7d2-192">d.</span><span class="sxs-lookup"><span data-stu-id="2f7d2-192">d.</span></span> <span data-ttu-id="2f7d2-193">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f7d2-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="2f7d2-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f7d2-195">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="2f7d2-197">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="2f7d2-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2f7d2-198">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f7d2-200">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f7d2-202">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f7d2-204">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2f7d2-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f7d2-206">a.</span><span class="sxs-lookup"><span data-stu-id="2f7d2-206">a.</span></span> <span data-ttu-id="2f7d2-207">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f7d2-208">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-208">b.</span></span> <span data-ttu-id="2f7d2-209">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f7d2-210">c.</span><span class="sxs-lookup"><span data-stu-id="2f7d2-210">c.</span></span> <span data-ttu-id="2f7d2-211">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2f7d2-212">d.</span><span class="sxs-lookup"><span data-stu-id="2f7d2-212">d.</span></span> <span data-ttu-id="2f7d2-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="2f7d2-214">建立 PlanMyLeave 測試使用者</span><span class="sxs-lookup"><span data-stu-id="2f7d2-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="2f7d2-215">本節目標是在 PlanMyLeave 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="2f7d2-216">PlanMyLeave 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="2f7d2-217">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-217">There is no action item for you in this section.</span></span> <span data-ttu-id="2f7d2-218">嘗試存取 PlanMyLeave 時，如果使用者還不存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="2f7d2-219">如果您需要手動建立使用者，就必須連絡 [PlanMyLeave 支援小組](mailto:support@planmyleave.com)。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2f7d2-220">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="2f7d2-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2f7d2-221">在本節中，您會將 PlanMyLeave 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span></span>

![指派使用者][200] 

<span data-ttu-id="2f7d2-223">**若要將 Britta Simon 指派給 PlanMyLeave，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="2f7d2-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="2f7d2-224">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="2f7d2-226">在應用程式清單中，選取 **PlanMyLeave**。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-226">In the applications list, select **PlanMyLeave**.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="2f7d2-228">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-228">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="2f7d2-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-230">Click **Add** button.</span></span> <span data-ttu-id="2f7d2-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="2f7d2-233">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2f7d2-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f7d2-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="2f7d2-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="2f7d2-236">Testing single sign-on</span></span>

<span data-ttu-id="2f7d2-237">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2f7d2-238">當您在「存取面板」中按一下 [PlanMyLeave] 圖格時，應該會自動登入您的 PlanMyLeave 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f7d2-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2f7d2-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="2f7d2-239">Additional resources</span></span>

* [<span data-ttu-id="2f7d2-240">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="2f7d2-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f7d2-241">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="2f7d2-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png