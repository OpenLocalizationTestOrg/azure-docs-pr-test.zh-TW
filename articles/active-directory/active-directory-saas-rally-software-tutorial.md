---
title: "教學課程：Azure Active Directory 與 Rally Software 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Rally Software 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: 6481c9ef0ca71419ccfa6f7956f4702985743df3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="32a13-103">教學課程：Azure Active Directory 與 Rally Software 整合</span><span class="sxs-lookup"><span data-stu-id="32a13-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="32a13-104">在此教學課程中，您將了解如何整合 Rally Software 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="32a13-104">In this tutorial, you learn how to integrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32a13-105">Rally Software 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="32a13-105">Integrating Rally Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="32a13-106">您可以在 Azure AD 中控制可存取 Rally Software 的人員。</span><span class="sxs-lookup"><span data-stu-id="32a13-106">You can control in Azure AD who has access to Rally Software.</span></span>
- <span data-ttu-id="32a13-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Rally Software (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="32a13-107">You can enable your users to automatically get signed-on to Rally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="32a13-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="32a13-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="32a13-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="32a13-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32a13-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="32a13-110">Prerequisites</span></span>

<span data-ttu-id="32a13-111">若要設定 Azure AD 與 Rally Software 整合，您需要以下項目：</span><span class="sxs-lookup"><span data-stu-id="32a13-111">To configure Azure AD integration with Rally Software, you need the following items:</span></span>

- <span data-ttu-id="32a13-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="32a13-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32a13-113">已啟用 Rally Software 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="32a13-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32a13-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="32a13-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32a13-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="32a13-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32a13-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="32a13-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32a13-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="32a13-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32a13-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="32a13-118">Scenario description</span></span>
<span data-ttu-id="32a13-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="32a13-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32a13-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="32a13-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32a13-121">從資源庫新增 Rally Software</span><span class="sxs-lookup"><span data-stu-id="32a13-121">Adding Rally Software from the gallery</span></span>
2. <span data-ttu-id="32a13-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="32a13-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-the-gallery"></a><span data-ttu-id="32a13-123">從資源庫新增 Rally Software</span><span class="sxs-lookup"><span data-stu-id="32a13-123">Adding Rally Software from the gallery</span></span>
<span data-ttu-id="32a13-124">若要設定將 Rally Software 整合到 Azure AD 中，您需要從資源庫將 Rally Software 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="32a13-124">To configure the integration of Rally Software into Azure AD, you need to add Rally Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32a13-125">**若要從資源庫新增 Rally Software，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="32a13-125">**To add Rally Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32a13-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="32a13-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="32a13-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="32a13-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="32a13-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="32a13-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="32a13-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32a13-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="32a13-133">在搜尋方塊中，輸入 **Rally Software**，從結果面板中選取 [Rally Software]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="32a13-133">In the search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="32a13-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="32a13-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="32a13-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Rally Software 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="32a13-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32a13-137">單一登入若要運作，Azure AD 必須知道 Rally Software 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="32a13-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rally Software is to a user in Azure AD.</span></span> <span data-ttu-id="32a13-138">換句話說，Azure AD 使用者和 Rally Software 中的相關使用者之間必須建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="32a13-138">In other words, a link relationship between an Azure AD user and the related user in Rally Software needs to be established.</span></span>

<span data-ttu-id="32a13-139">在 Rally Software 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="32a13-139">In Rally Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="32a13-140">若要設定及測試與 Rally Software 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="32a13-140">To configure and test Azure AD single sign-on with Rally Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32a13-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="32a13-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="32a13-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="32a13-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32a13-143">**[建立 Rally Software 測試使用者](#create-a-rally-software-test-user)** - 在 Rally Software 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="32a13-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - to have a counterpart of Britta Simon in Rally Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="32a13-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="32a13-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32a13-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="32a13-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="32a13-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="32a13-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="32a13-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Rally Software 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="32a13-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="32a13-148">**若要使用 Rally Software 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="32a13-148">**To configure Azure AD single sign-on with Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="32a13-149">在 Azure 入口網站的 [Rally Software] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="32a13-149">In the Azure portal, on the **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="32a13-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="32a13-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="32a13-153">在 [Rally Software 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="32a13-153">On the **Rally Software Domain and URLs** section, perform the following steps:</span></span>

    ![Rally Software 網域與 URL 單一登入資訊](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="32a13-155">a.</span><span class="sxs-lookup"><span data-stu-id="32a13-155">a.</span></span> <span data-ttu-id="32a13-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="32a13-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="32a13-157">b.</span><span class="sxs-lookup"><span data-stu-id="32a13-157">b.</span></span> <span data-ttu-id="32a13-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="32a13-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32a13-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="32a13-159">These values are not real.</span></span> <span data-ttu-id="32a13-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="32a13-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="32a13-161">請連絡 [Rally Software 用戶端支援小組](https://help.rallydev.com/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="32a13-161">Contact [Rally Software Client support team](https://help.rallydev.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="32a13-162">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="32a13-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="32a13-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="32a13-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32a13-166">在 [Rally Software 設定] 區段上，按一下 [設定 Rally Software] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="32a13-166">On the **Rally Software Configuration** section, click **Configure Rally Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="32a13-167">從 [快速參考] 區段中複製 [登出 URL] 和 [SAML 實體識別碼]。</span><span class="sxs-lookup"><span data-stu-id="32a13-167">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Rally Software 設定](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="32a13-169">登入您的 **Rally Software** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="32a13-169">Log in to your **Rally Software** tenant.</span></span>

8. <span data-ttu-id="32a13-170">在頂端工具列中，按一下 [設定]，然後選取 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="32a13-170">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="32a13-171">![訂用帳戶](./media/active-directory-saas-rally-software-tutorial/ic769531.png "訂用帳戶")</span><span class="sxs-lookup"><span data-stu-id="32a13-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="32a13-172">按一下 [動作] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32a13-172">Click the **Action** button.</span></span> <span data-ttu-id="32a13-173">選取工具列右上方的 [編輯訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="32a13-173">Select **Edit Subscription** at the top right side of the toolbar.</span></span>

10. <span data-ttu-id="32a13-174">在 [訂用帳戶] 對話方塊頁面上，執行下列步驟，然後按一下 [儲存並關閉]：</span><span class="sxs-lookup"><span data-stu-id="32a13-174">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="32a13-175">![驗證](./media/active-directory-saas-rally-software-tutorial/ic769542.png "驗證")</span><span class="sxs-lookup"><span data-stu-id="32a13-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="32a13-176">a.</span><span class="sxs-lookup"><span data-stu-id="32a13-176">a.</span></span> <span data-ttu-id="32a13-177">從 [驗證] 下拉式清單中選取 [Rally 或 SSO 驗證]。</span><span class="sxs-lookup"><span data-stu-id="32a13-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="32a13-178">b.</span><span class="sxs-lookup"><span data-stu-id="32a13-178">b.</span></span> <span data-ttu-id="32a13-179">在 [識別提供者 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="32a13-179">In the **Identity provider URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="32a13-180">c.</span><span class="sxs-lookup"><span data-stu-id="32a13-180">c.</span></span> <span data-ttu-id="32a13-181">在 [SSO 登出] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="32a13-181">In the **SSO Logout** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="32a13-182">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="32a13-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="32a13-183">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="32a13-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="32a13-184">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32a13-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="32a13-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="32a13-185">Create an Azure AD test user</span></span>

<span data-ttu-id="32a13-186">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="32a13-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="32a13-188">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="32a13-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32a13-189">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32a13-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="32a13-191">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="32a13-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="32a13-193">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="32a13-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="32a13-195">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="32a13-195">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="32a13-197">a.</span><span class="sxs-lookup"><span data-stu-id="32a13-197">a.</span></span> <span data-ttu-id="32a13-198">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="32a13-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32a13-199">b.</span><span class="sxs-lookup"><span data-stu-id="32a13-199">b.</span></span> <span data-ttu-id="32a13-200">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="32a13-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="32a13-201">c.</span><span class="sxs-lookup"><span data-stu-id="32a13-201">c.</span></span> <span data-ttu-id="32a13-202">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="32a13-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="32a13-203">d.</span><span class="sxs-lookup"><span data-stu-id="32a13-203">d.</span></span> <span data-ttu-id="32a13-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="32a13-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="32a13-205">建立 Rally Software 測試使用者</span><span class="sxs-lookup"><span data-stu-id="32a13-205">Create a Rally Software test user</span></span>

<span data-ttu-id="32a13-206">若要讓 Azure AD 使用者可以登入，則必須使用他們的 Azure Active Directory 使用者名稱將其佈建至 Rally Software 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32a13-206">For Azure AD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="32a13-207">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="32a13-207">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="32a13-208">登入您的 Rally Software 租用戶。</span><span class="sxs-lookup"><span data-stu-id="32a13-208">Log in to your Rally Software tenant.</span></span>

2. <span data-ttu-id="32a13-209">按一下 [設定] \> [使用者]，然後按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="32a13-209">Go to **Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="32a13-210">![使用者](./media/active-directory-saas-rally-software-tutorial/ic781039.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="32a13-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="32a13-211">在 [新使用者] 文字方塊中輸入名稱，然後按一下 [新增詳細資料] 。</span><span class="sxs-lookup"><span data-stu-id="32a13-211">Type the name in the New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="32a13-212">在 [建立使用者]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="32a13-212">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="32a13-213">![建立使用者](./media/active-directory-saas-rally-software-tutorial/ic781040.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="32a13-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="32a13-214">a.</span><span class="sxs-lookup"><span data-stu-id="32a13-214">a.</span></span> <span data-ttu-id="32a13-215">在 [使用者名稱] 文字方塊中，輸入使用者的名稱，例如 **Brittsimon**。</span><span class="sxs-lookup"><span data-stu-id="32a13-215">In the **User Name** textbox, type the name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="32a13-216">b.</span><span class="sxs-lookup"><span data-stu-id="32a13-216">b.</span></span> <span data-ttu-id="32a13-217">在 [電子郵件地址] 文字方塊中，輸入使用者的電子郵件，例如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="32a13-217">In **E-mail Address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="32a13-218">c.</span><span class="sxs-lookup"><span data-stu-id="32a13-218">c.</span></span> <span data-ttu-id="32a13-219">在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="32a13-219">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="32a13-220">d.</span><span class="sxs-lookup"><span data-stu-id="32a13-220">d.</span></span> <span data-ttu-id="32a13-221">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="32a13-221">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="32a13-222">e.</span><span class="sxs-lookup"><span data-stu-id="32a13-222">e.</span></span> <span data-ttu-id="32a13-223">按一下 [儲存並關閉]。</span><span class="sxs-lookup"><span data-stu-id="32a13-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="32a13-224">您可以使用任何其他的 Rally Software 使用者帳戶建立工具或 Rally Software 提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="32a13-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="32a13-225">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="32a13-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="32a13-226">在本節中，您會將 Rally Software 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="32a13-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rally Software.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="32a13-228">**若要指派 Britta Simon 到 Rally Software，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="32a13-228">**To assign Britta Simon to Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="32a13-229">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="32a13-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="32a13-231">在應用程式清單中，選取 [Rally Software]。</span><span class="sxs-lookup"><span data-stu-id="32a13-231">In the applications list, select **Rally Software**.</span></span>

    ![應用程式清單中的 Rally Software 連結](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="32a13-233">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="32a13-233">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="32a13-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32a13-235">Click **Add** button.</span></span> <span data-ttu-id="32a13-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="32a13-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="32a13-238">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="32a13-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="32a13-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32a13-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32a13-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32a13-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="32a13-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="32a13-241">Test single sign-on</span></span>

<span data-ttu-id="32a13-242">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="32a13-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="32a13-243">當您在 [存取面板] 中按一下 [Rally Software] 圖格時，應該會自動登入您的 Rally Software 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32a13-243">When you click the Rally Software tile in the Access Panel, you should get automatically signed-on to your Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32a13-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="32a13-244">Additional resources</span></span>

* [<span data-ttu-id="32a13-245">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="32a13-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32a13-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="32a13-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

