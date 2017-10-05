---
title: "教學課程：Azure Active Directory 與 YouEarnedIt 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 YouEarnedIt 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: c29d218dbca581f102caf8070fa40894e7006e71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="e07fd-103">教學課程：Azure Active Directory 與 YouEarnedIt 整合</span><span class="sxs-lookup"><span data-stu-id="e07fd-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="e07fd-104">在本教學課程中，您會了解如何整合 YouEarnedIt 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e07fd-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e07fd-105">YouEarnedIt 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="e07fd-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e07fd-106">您可以在 Azure AD 中控制可存取 YouEarnedIt 的人員。</span><span class="sxs-lookup"><span data-stu-id="e07fd-106">You can control in Azure AD who has access to YouEarnedIt.</span></span>
- <span data-ttu-id="e07fd-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 YouEarnedIt (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="e07fd-107">You can enable your users to automatically get signed-on to YouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e07fd-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="e07fd-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e07fd-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e07fd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e07fd-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e07fd-110">Prerequisites</span></span>

<span data-ttu-id="e07fd-111">若要設定與 YouEarnedIt 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e07fd-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span></span>

- <span data-ttu-id="e07fd-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e07fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e07fd-113">已啟用 YouEarnedIt 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e07fd-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e07fd-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e07fd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e07fd-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e07fd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e07fd-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e07fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e07fd-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e07fd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e07fd-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e07fd-118">Scenario description</span></span>
<span data-ttu-id="e07fd-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e07fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e07fd-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="e07fd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e07fd-121">從資源庫新增 YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="e07fd-121">Adding YouEarnedIt from the gallery</span></span>
2. <span data-ttu-id="e07fd-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e07fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-the-gallery"></a><span data-ttu-id="e07fd-123">從資源庫新增 YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="e07fd-123">Adding YouEarnedIt from the gallery</span></span>
<span data-ttu-id="e07fd-124">若要設定 YouEarnedIt 與 Azure AD 整合，您需要從資源庫將 YouEarnedIt 加入到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="e07fd-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e07fd-125">**若要從資源庫加入 YouEarnedIt，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e07fd-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e07fd-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e07fd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="e07fd-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e07fd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e07fd-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e07fd-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="e07fd-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e07fd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="e07fd-133">在搜尋方塊中，輸入 **YouEarnedt**，從結果面板中選取 [YouEarnedt]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="e07fd-133">In the search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e07fd-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e07fd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e07fd-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 YouEarnedIt 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e07fd-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e07fd-137">若要讓單一登入運作，Azure AD 必須知道 YouEarnedIt 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="e07fd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span></span> <span data-ttu-id="e07fd-138">換句話說，必須建立 Azure AD 使用者和 YouEarnedIt 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e07fd-138">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span></span>

<span data-ttu-id="e07fd-139">將 Azure AD 中 [使用者名稱] 的值指派為 YouEarnedIt 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e07fd-139">In YouEarnedIt, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e07fd-140">若要設定及測試對 YouEarnedIt 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e07fd-140">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e07fd-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="e07fd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e07fd-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e07fd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e07fd-143">**[建立 YouEarnedIt 測試使用者](#create-a-youearnedit-test-user)** - 在 YouEarnedIt 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="e07fd-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e07fd-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e07fd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e07fd-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="e07fd-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e07fd-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e07fd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e07fd-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 YouEarnedIt 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e07fd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="e07fd-148">**若要設定與 YouEarnedIt 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e07fd-148">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="e07fd-149">在 Azure 入口網站的 [YouEarnedIt] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e07fd-149">In the Azure portal, on the **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="e07fd-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="e07fd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="e07fd-153">在 [YouEarnedIt 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e07fd-153">On the **YouEarnedIt Domain and URLs** section, perform the following steps:</span></span>

    ![YouEarnedIt 網域與 URL 單一登入資訊](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="e07fd-155">a.</span><span class="sxs-lookup"><span data-stu-id="e07fd-155">a.</span></span> <span data-ttu-id="e07fd-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰</span><span class="sxs-lookup"><span data-stu-id="e07fd-156">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | <span data-ttu-id="e07fd-157">環境</span><span class="sxs-lookup"><span data-stu-id="e07fd-157">Environment</span></span>  | <span data-ttu-id="e07fd-158">模式</span><span class="sxs-lookup"><span data-stu-id="e07fd-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="e07fd-159">Production</span><span class="sxs-lookup"><span data-stu-id="e07fd-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="e07fd-160">沙箱</span><span class="sxs-lookup"><span data-stu-id="e07fd-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="e07fd-161">b.</span><span class="sxs-lookup"><span data-stu-id="e07fd-161">b.</span></span> <span data-ttu-id="e07fd-162">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="e07fd-162">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="e07fd-163">環境</span><span class="sxs-lookup"><span data-stu-id="e07fd-163">Environment</span></span>  | <span data-ttu-id="e07fd-164">模式</span><span class="sxs-lookup"><span data-stu-id="e07fd-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="e07fd-165">Production</span><span class="sxs-lookup"><span data-stu-id="e07fd-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="e07fd-166">沙箱</span><span class="sxs-lookup"><span data-stu-id="e07fd-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="e07fd-167">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="e07fd-167">These values are not real.</span></span> <span data-ttu-id="e07fd-168">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="e07fd-168">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e07fd-169">請連絡 [YouEarnedIt 客戶支援小組](https://youearnedit.freshdesk.com/support/tickets/new)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="e07fd-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) to get these values.</span></span> 
 
4. <span data-ttu-id="e07fd-170">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e07fd-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="e07fd-172">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e07fd-172">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e07fd-174">在 [YouEarnedIt 組態] 區段上，按一下 [設定 YouEarnedIt] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="e07fd-174">On the **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e07fd-175">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="e07fd-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![YouEarnedIt 組態](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="e07fd-177">若要在 **YouEarnedIt** 端設定單一登入，您必須將已下載的「憑證 (Base64)」和「SAML 單一登入服務 URL」傳送給 [YouEarnedIt 支援小組](https://youearnedit.freshdesk.com/support/tickets/new)。</span><span class="sxs-lookup"><span data-stu-id="e07fd-177">To configure single sign-on on **YouEarnedIt** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="e07fd-178">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="e07fd-178">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e07fd-179">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="e07fd-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e07fd-180">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="e07fd-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e07fd-181">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e07fd-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e07fd-182">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e07fd-182">Create an Azure AD test user</span></span>

<span data-ttu-id="e07fd-183">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e07fd-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="e07fd-185">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e07fd-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e07fd-186">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e07fd-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e07fd-188">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e07fd-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e07fd-190">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e07fd-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e07fd-192">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e07fd-192">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e07fd-194">a.</span><span class="sxs-lookup"><span data-stu-id="e07fd-194">a.</span></span> <span data-ttu-id="e07fd-195">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e07fd-195">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e07fd-196">b.</span><span class="sxs-lookup"><span data-stu-id="e07fd-196">b.</span></span> <span data-ttu-id="e07fd-197">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="e07fd-197">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e07fd-198">c.</span><span class="sxs-lookup"><span data-stu-id="e07fd-198">c.</span></span> <span data-ttu-id="e07fd-199">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="e07fd-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e07fd-200">d.</span><span class="sxs-lookup"><span data-stu-id="e07fd-200">d.</span></span> <span data-ttu-id="e07fd-201">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e07fd-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="e07fd-202">建立 YouEarnedIt 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e07fd-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="e07fd-203">在本節中，您要在 YouEarnedIt 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="e07fd-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="e07fd-204">請與 YouEarnedIt 支援小組合作，在 YouEarnedIt 平台中加入使用者。</span><span class="sxs-lookup"><span data-stu-id="e07fd-204">Please work with YouEarnedIt support team to add the users in the YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="e07fd-205">YouEarnedIt 預期識別提供者會在 NameID 屬性中提供 EmailAddress 或 UserName。</span><span class="sxs-lookup"><span data-stu-id="e07fd-205">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span></span> <span data-ttu-id="e07fd-206">如果在資料庫中找不到對應的 UserName 或 EmailAddress 或者不完全相符，則驗證會失敗。</span><span class="sxs-lookup"><span data-stu-id="e07fd-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span></span> <span data-ttu-id="e07fd-207">這會要求在 SSO 整合之前，將帳戶匯入 YouEarnedIt 系統 (通常透過 API 或 CSV 匯入)。</span><span class="sxs-lookup"><span data-stu-id="e07fd-207">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e07fd-208">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e07fd-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="e07fd-209">在本節中，您會將 YouEarnedIt 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e07fd-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YouEarnedIt.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="e07fd-211">**若要將 Britta Simon 指派到 YouEarnedIt，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="e07fd-211">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="e07fd-212">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e07fd-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e07fd-214">在應用程式清單中，選取 [YouEarnedIt] 。</span><span class="sxs-lookup"><span data-stu-id="e07fd-214">In the applications list, select **YouEarnedIt**.</span></span>

    ![應用程式清單中的 YouEarnedIt 連結](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="e07fd-216">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e07fd-216">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="e07fd-218">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e07fd-218">Click **Add** button.</span></span> <span data-ttu-id="e07fd-219">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e07fd-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="e07fd-221">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="e07fd-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e07fd-222">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e07fd-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e07fd-223">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e07fd-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e07fd-224">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e07fd-224">Test single sign-on</span></span>

<span data-ttu-id="e07fd-225">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="e07fd-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e07fd-226">當您在存取面板中按一下 YouEarnedIt 圖格時，應該會自動登入您的 YouEarnedIt 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e07fd-226">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span></span>
<span data-ttu-id="e07fd-227">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e07fd-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e07fd-228">其他資源</span><span class="sxs-lookup"><span data-stu-id="e07fd-228">Additional resources</span></span>

* [<span data-ttu-id="e07fd-229">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="e07fd-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e07fd-230">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e07fd-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

