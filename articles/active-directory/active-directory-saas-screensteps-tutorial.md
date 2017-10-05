---
title: "教學課程：Azure Active Directory 與 ScreenSteps 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ScreenSteps 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: b6ded8ba1adf03fdccbdb7573c09fae1857c8b16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="029f6-103">教學課程：Azure Active Directory 與 ScreenSteps 整合</span><span class="sxs-lookup"><span data-stu-id="029f6-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="029f6-104">在本教學課程中，您會了解如何將 ScreenSteps 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="029f6-104">In this tutorial, you learn how to integrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="029f6-105">ScreenSteps 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="029f6-105">Integrating ScreenSteps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="029f6-106">您可以在 Azure AD 中管控可存取 ScreenSteps 的人員。</span><span class="sxs-lookup"><span data-stu-id="029f6-106">You can control in Azure AD who has access to ScreenSteps.</span></span>
- <span data-ttu-id="029f6-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 ScreenSteps (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="029f6-107">You can enable your users to automatically get signed-on to ScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="029f6-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="029f6-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="029f6-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="029f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="029f6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="029f6-110">Prerequisites</span></span>

<span data-ttu-id="029f6-111">若要設定 Azure AD 與 ScreenSteps 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="029f6-111">To configure Azure AD integration with ScreenSteps, you need the following items:</span></span>

- <span data-ttu-id="029f6-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="029f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="029f6-113">已啟用 ScreenSteps 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="029f6-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="029f6-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="029f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="029f6-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="029f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="029f6-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="029f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="029f6-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="029f6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="029f6-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="029f6-118">Scenario description</span></span>
<span data-ttu-id="029f6-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="029f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="029f6-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="029f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="029f6-121">從資源庫新增 ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="029f6-121">Adding ScreenSteps from the gallery</span></span>
2. <span data-ttu-id="029f6-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="029f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-the-gallery"></a><span data-ttu-id="029f6-123">從資源庫新增 ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="029f6-123">Adding ScreenSteps from the gallery</span></span>
<span data-ttu-id="029f6-124">若要設定將 ScreenSteps 整合到 Azure AD 中，您需要從資源庫中，將 ScreenSteps 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="029f6-124">To configure the integration of ScreenSteps into Azure AD, you need to add ScreenSteps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="029f6-125">**若要從資源庫新增 ScreenSteps，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="029f6-125">**To add ScreenSteps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="029f6-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="029f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="029f6-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="029f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="029f6-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="029f6-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="029f6-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="029f6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="029f6-133">在搜尋方塊中，輸入 **ScreenSteps**，從結果面板中選取 [ScreenSteps]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="029f6-133">In the search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="029f6-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="029f6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="029f6-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 ScreenSteps 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="029f6-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="029f6-137">若要讓單一登入能夠運作，Azure AD 必須知道 ScreenSteps 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="029f6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ScreenSteps is to a user in Azure AD.</span></span> <span data-ttu-id="029f6-138">換句話說，必須在 Azure AD 使用者和 ScreenSteps 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="029f6-138">In other words, a link relationship between an Azure AD user and the related user in ScreenSteps needs to be established.</span></span>

<span data-ttu-id="029f6-139">在 ScreenSteps 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="029f6-139">In ScreenSteps, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="029f6-140">若要使用 ScreenSteps 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="029f6-140">To configure and test Azure AD single sign-on with ScreenSteps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="029f6-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="029f6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="029f6-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="029f6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="029f6-143">**[建立 ScreenSteps 測試使用者](#create-a-screensteps-test-user)** - 在 ScreenSteps 中建立 Britta Simon 的對應項目，且該項目須與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="029f6-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - to have a counterpart of Britta Simon in ScreenSteps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="029f6-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="029f6-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="029f6-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="029f6-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="029f6-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="029f6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="029f6-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 ScreenSteps 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="029f6-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="029f6-148">**若要使用 ScreenSteps 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="029f6-148">**To configure Azure AD single sign-on with ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="029f6-149">在 Azure 入口網站的 [ScreenSteps] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="029f6-149">In the Azure portal, on the **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="029f6-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="029f6-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="029f6-153">在 [ScreenSteps 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="029f6-153">On the **ScreenSteps Domain and URLs** section, perform the following steps:</span></span>

    ![ScreenSteps 網域及 URL 單一登入資訊](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="029f6-155">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="029f6-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="029f6-156">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="029f6-156">This value is not real.</span></span> <span data-ttu-id="029f6-157">使用實際的「登入 URL」來更新此值，稍後會在本教學課程中說明。</span><span class="sxs-lookup"><span data-stu-id="029f6-157">Update this value with the actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="029f6-158">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="029f6-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="029f6-160">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="029f6-160">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="029f6-162">在 [ScreenSteps 設定] 區段上，按一下 [設定 ScreenSteps] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="029f6-162">On the **ScreenSteps Configuration** section, click **Configure ScreenSteps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="029f6-163">從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="029f6-163">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![ScreenSteps 設定](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="029f6-165">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 ScreenSteps 公司網站。</span><span class="sxs-lookup"><span data-stu-id="029f6-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="029f6-166">按一下 [帳戶設定]。</span><span class="sxs-lookup"><span data-stu-id="029f6-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="029f6-167">![帳戶管理](./media/active-directory-saas-screensteps-tutorial/ic778523.png "帳戶管理")</span><span class="sxs-lookup"><span data-stu-id="029f6-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="029f6-168">按一下 [單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="029f6-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="029f6-169">![遠端驗證](./media/active-directory-saas-screensteps-tutorial/ic778524.png "遠端驗證")</span><span class="sxs-lookup"><span data-stu-id="029f6-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="029f6-170">按一下 [建立單一登入端點]。</span><span class="sxs-lookup"><span data-stu-id="029f6-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="029f6-171">![遠端驗證](./media/active-directory-saas-screensteps-tutorial/ic778525.png "遠端驗證")</span><span class="sxs-lookup"><span data-stu-id="029f6-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="029f6-172">在 [建立單一登入端點] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="029f6-172">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="029f6-173">![建立驗證端點](./media/active-directory-saas-screensteps-tutorial/ic778526.png "建立驗證端點")</span><span class="sxs-lookup"><span data-stu-id="029f6-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="029f6-174">a.</span><span class="sxs-lookup"><span data-stu-id="029f6-174">a.</span></span> <span data-ttu-id="029f6-175">在 [標題]  文字方塊中輸入標題。</span><span class="sxs-lookup"><span data-stu-id="029f6-175">In the **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="029f6-176">b.</span><span class="sxs-lookup"><span data-stu-id="029f6-176">b.</span></span> <span data-ttu-id="029f6-177">從 [模式] 清單中選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="029f6-177">From the **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="029f6-178">c.</span><span class="sxs-lookup"><span data-stu-id="029f6-178">c.</span></span> <span data-ttu-id="029f6-179">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="029f6-179">Click **Create**.</span></span>

12. <span data-ttu-id="029f6-180">**編輯**新的端點。</span><span class="sxs-lookup"><span data-stu-id="029f6-180">**Edit** the new endpoint.</span></span>

    <span data-ttu-id="029f6-181">![編輯端點](./media/active-directory-saas-screensteps-tutorial/ic778528.png "編輯端點")</span><span class="sxs-lookup"><span data-stu-id="029f6-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="029f6-182">在 [編輯單一登入端點] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="029f6-182">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="029f6-183">![遠端驗證端點](./media/active-directory-saas-screensteps-tutorial/ic778527.png "遠端驗證端點")</span><span class="sxs-lookup"><span data-stu-id="029f6-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="029f6-184">a.</span><span class="sxs-lookup"><span data-stu-id="029f6-184">a.</span></span> <span data-ttu-id="029f6-185">按一下 [上傳新的 SAML 憑證檔案]，然後上傳您從 Azure 入口網站下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="029f6-185">Click **Upload new SAML Certificate file**, and then upload the certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="029f6-186">b.</span><span class="sxs-lookup"><span data-stu-id="029f6-186">b.</span></span> <span data-ttu-id="029f6-187">將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值，貼到 [遠端登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="029f6-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="029f6-188">c.</span><span class="sxs-lookup"><span data-stu-id="029f6-188">c.</span></span> <span data-ttu-id="029f6-189">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="029f6-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="029f6-190">d.</span><span class="sxs-lookup"><span data-stu-id="029f6-190">d.</span></span> <span data-ttu-id="029f6-191">選取要在佈建使用者時將使用者指派給哪個 [群組]。</span><span class="sxs-lookup"><span data-stu-id="029f6-191">Select a **Group** to assign users to when they are provisioned.</span></span>
    
    <span data-ttu-id="029f6-192">e.</span><span class="sxs-lookup"><span data-stu-id="029f6-192">e.</span></span> <span data-ttu-id="029f6-193">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="029f6-193">Click **Update**.</span></span>

    <span data-ttu-id="029f6-194">f.</span><span class="sxs-lookup"><span data-stu-id="029f6-194">f.</span></span> <span data-ttu-id="029f6-195">將 [SAML 取用者 URL] 複製到剪貼簿，並且貼至 [ScreenSteps 網域和 URL] 區段中的 [登出 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="029f6-195">Copy the **SAML Consumer URL** to the clipboard and paste in to the **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="029f6-196">g.</span><span class="sxs-lookup"><span data-stu-id="029f6-196">g.</span></span> <span data-ttu-id="029f6-197">返回 [編輯單一登入端點]。</span><span class="sxs-lookup"><span data-stu-id="029f6-197">Return to the **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="029f6-198">h.</span><span class="sxs-lookup"><span data-stu-id="029f6-198">h.</span></span> <span data-ttu-id="029f6-199">按一下 [設為帳戶的預設值] 按鈕，讓所有登入 ScreenSteps 的使用者使用此端點。</span><span class="sxs-lookup"><span data-stu-id="029f6-199">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="029f6-200">或者，您可以按一下 [新增至網站] 按鈕，以對 **ScreenSteps** 中的特定站台使用此端點。</span><span class="sxs-lookup"><span data-stu-id="029f6-200">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="029f6-201">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="029f6-201">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="029f6-202">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="029f6-202">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="029f6-203">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="029f6-203">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="029f6-204">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="029f6-204">Create an Azure AD test user</span></span>

<span data-ttu-id="029f6-205">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="029f6-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="029f6-207">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="029f6-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="029f6-208">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="029f6-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="029f6-210">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="029f6-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="029f6-212">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="029f6-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="029f6-214">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="029f6-214">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="029f6-216">a.</span><span class="sxs-lookup"><span data-stu-id="029f6-216">a.</span></span> <span data-ttu-id="029f6-217">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="029f6-217">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="029f6-218">b.</span><span class="sxs-lookup"><span data-stu-id="029f6-218">b.</span></span> <span data-ttu-id="029f6-219">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="029f6-219">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="029f6-220">c.</span><span class="sxs-lookup"><span data-stu-id="029f6-220">c.</span></span> <span data-ttu-id="029f6-221">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="029f6-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="029f6-222">d.</span><span class="sxs-lookup"><span data-stu-id="029f6-222">d.</span></span> <span data-ttu-id="029f6-223">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="029f6-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="029f6-224">建立 ScreenSteps 測試使用者</span><span class="sxs-lookup"><span data-stu-id="029f6-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="029f6-225">在本節中，您要在 ScreenSteps 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="029f6-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="029f6-226">與 [ScreenSteps 用戶端支援小組](https://www.screensteps.com/contact)合作，在 ScreenSteps 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="029f6-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add the users in the ScreenSteps platform.</span></span> <span data-ttu-id="029f6-227">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="029f6-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="029f6-228">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="029f6-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="029f6-229">在本節中，您會將 ScreenSteps 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="029f6-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ScreenSteps.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="029f6-231">**若要將 Britta Simon 指派給 ScreenSteps，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="029f6-231">**To assign Britta Simon to ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="029f6-232">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="029f6-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="029f6-234">在應用程式清單中，選取 [ScreenSteps]。</span><span class="sxs-lookup"><span data-stu-id="029f6-234">In the applications list, select **ScreenSteps**.</span></span>

    ![應用程式清單中的 ScreenSteps 連結](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="029f6-236">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="029f6-236">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="029f6-238">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="029f6-238">Click **Add** button.</span></span> <span data-ttu-id="029f6-239">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="029f6-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="029f6-241">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="029f6-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="029f6-242">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="029f6-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="029f6-243">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="029f6-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="029f6-244">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="029f6-244">Test single sign-on</span></span>

<span data-ttu-id="029f6-245">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="029f6-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="029f6-246">當您在存取面板中按一下 [ScreenSteps] 圖格時，應該會自動登入您的 ScreenSteps 應用程式。</span><span class="sxs-lookup"><span data-stu-id="029f6-246">When you click the ScreenSteps tile in the Access Panel, you should get automatically signed-on to your ScreenSteps application.</span></span>
<span data-ttu-id="029f6-247">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="029f6-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="029f6-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="029f6-248">Additional resources</span></span>

* [<span data-ttu-id="029f6-249">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="029f6-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="029f6-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="029f6-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

