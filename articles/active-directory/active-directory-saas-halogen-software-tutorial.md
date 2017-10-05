---
title: "教學課程：Azure Active Directory 與 Halogen Software 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Halogen Software 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: e09fa93038965e4880a23002bac6917ad2a077f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="c4b5a-103">教學課程：Azure Active Directory 與 Halogen Software 整合</span><span class="sxs-lookup"><span data-stu-id="c4b5a-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="c4b5a-104">在此教學課程中，您將了解如何整合 Halogen Software 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4b5a-105">Halogen Software 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="c4b5a-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c4b5a-106">您可以在 Azure AD 中控制可存取 Halogen Software 的人員。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-106">You can control in Azure AD who has access to Halogen Software</span></span>
- <span data-ttu-id="c4b5a-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Halogen Software (單一登入)</span><span class="sxs-lookup"><span data-stu-id="c4b5a-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4b5a-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="c4b5a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c4b5a-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4b5a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c4b5a-110">Prerequisites</span></span>

<span data-ttu-id="c4b5a-111">若要設定 Azure AD 與 Halogen Software 整合，您需要以下項目：</span><span class="sxs-lookup"><span data-stu-id="c4b5a-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

- <span data-ttu-id="c4b5a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c4b5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4b5a-113">已啟用 Halogen Software 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c4b5a-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4b5a-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4b5a-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c4b5a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4b5a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4b5a-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4b5a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c4b5a-118">Scenario description</span></span>

<span data-ttu-id="c4b5a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4b5a-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="c4b5a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4b5a-121">從資源庫加入 Halogen Software</span><span class="sxs-lookup"><span data-stu-id="c4b5a-121">Adding Halogen Software from the gallery</span></span>
2. <span data-ttu-id="c4b5a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c4b5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="c4b5a-123">從資源庫加入 Halogen Software</span><span class="sxs-lookup"><span data-stu-id="c4b5a-123">Adding Halogen Software from the gallery</span></span>

<span data-ttu-id="c4b5a-124">若要設定 Halogen Software 與 Azure AD 整合，您需要從資源庫將 Halogen Software 加入 受管理 SaaS app 的清單。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c4b5a-125">**若要從資源庫新增 Halogen Software，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c4b5a-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b5a-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4b5a-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c4b5a-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c4b5a-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c4b5a-133">在搜尋方塊中，輸入 **Halogen Software**。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-133">In the search box, type **Halogen Software**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="c4b5a-135">在結果窗格中，選取 [Halogen Software]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4b5a-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c4b5a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4b5a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Halogen Software 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c4b5a-139">單一登入若要運作，Azure AD 必須知道 Halogen Software 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span></span> <span data-ttu-id="c4b5a-140">換句話說，Azure AD 使用者和 Halogen Software 中的相關使用者之間必須建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="c4b5a-141">在 Halogen Software 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c4b5a-142">若要使用 Halogen Software 設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c4b5a-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c4b5a-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c4b5a-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4b5a-145">**[建立 Halogen Software 測試使用者](#creating-a-halogen-software-test-user)** - 在 Halogen Software 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4b5a-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4b5a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4b5a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c4b5a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4b5a-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Halogen Software 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="c4b5a-150">**若要使用 Halogen Software 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c4b5a-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b5a-151">在 Azure 入口網站的 [Halogen Software] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c4b5a-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="c4b5a-155">在 [Halogen Software 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c4b5a-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="c4b5a-157">a.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-157">a.</span></span> <span data-ttu-id="c4b5a-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c4b5a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="c4b5a-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-159">b.</span></span> <span data-ttu-id="c4b5a-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://global.halogensoftware.com/<companyname>`、`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c4b5a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4b5a-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-161">These values are not real.</span></span> <span data-ttu-id="c4b5a-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c4b5a-163">請連絡 [Halogen Software 用戶端支援小組](https://support.halogensoftware.com/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="c4b5a-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="c4b5a-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4b5a-168">在不同的瀏覽器視窗中，以系統管理員身分登入您的 **Halogen Software** 。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="c4b5a-169">按一下 [選項]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-169">Click the **Options** tab.</span></span> 
   
    ![何謂 Azure AD Connect][12]

8. <span data-ttu-id="c4b5a-171">在左瀏覽窗格中，按一下 [SAML 組態] 。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-171">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![何謂 Azure AD Connect][13]

9. <span data-ttu-id="c4b5a-173">在 [SAML 組態]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c4b5a-173">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![何謂 Azure AD Connect][14]

     <span data-ttu-id="c4b5a-175">a.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-175">a.</span></span> <span data-ttu-id="c4b5a-176">對於 [唯一識別碼]，選取 [NameID]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="c4b5a-177">b.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-177">b.</span></span> <span data-ttu-id="c4b5a-178">對於 [唯一識別碼對應到]，選取 [Username]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="c4b5a-179">c.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-179">c.</span></span> <span data-ttu-id="c4b5a-180">若要更新您已下載的中繼資料檔，請按一下 [瀏覽] 來選取檔案，然後按一下 [上傳檔案]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="c4b5a-181">d.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-181">d.</span></span> <span data-ttu-id="c4b5a-182">若要測試組態，請按一下 [執行測試]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-182">To test the configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="c4b5a-183">您需要等候「SAML 測試已完成。請關閉此視窗。」訊息顯示。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="c4b5a-184">然後關閉已開啟的瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-184">Then, close the opened browser window.</span></span> <span data-ttu-id="c4b5a-185">完成測試之後才會啟用 [啟用 SAML] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
     
     <span data-ttu-id="c4b5a-186">e.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-186">e.</span></span> <span data-ttu-id="c4b5a-187">選取 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="c4b5a-188">f.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-188">f.</span></span> <span data-ttu-id="c4b5a-189">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="c4b5a-190">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="c4b5a-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c4b5a-191">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c4b5a-192">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4b5a-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4b5a-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c4b5a-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="c4b5a-194">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c4b5a-196">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c4b5a-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b5a-197">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4b5a-199">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4b5a-201">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4b5a-203">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c4b5a-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4b5a-205">a.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-205">a.</span></span> <span data-ttu-id="c4b5a-206">在 [名稱] 文字方塊中，輸入 **BrittaSimon** 作為名稱。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-206">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="c4b5a-207">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-207">b.</span></span> <span data-ttu-id="c4b5a-208">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4b5a-209">c.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-209">c.</span></span> <span data-ttu-id="c4b5a-210">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c4b5a-211">d.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-211">d.</span></span> <span data-ttu-id="c4b5a-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="c4b5a-213">建立 Halogen Software 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c4b5a-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="c4b5a-214">本節目標是在 Halogen Software 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="c4b5a-215">**若要建立名為 Britta Simon 的使用者，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="c4b5a-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b5a-216">以系統管理員身分登入您的 **Halogen Software** 。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-216">Sign on to your **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="c4b5a-217">按一下 [使用者中心] 索引標籤，然後按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-217">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![何謂 Azure AD Connect][300]  

3. <span data-ttu-id="c4b5a-219">在 [新增使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c4b5a-219">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![何謂 Azure AD Connect][301]

    <span data-ttu-id="c4b5a-221">a.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-221">a.</span></span> <span data-ttu-id="c4b5a-222">在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-222">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>
    
    <span data-ttu-id="c4b5a-223">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-223">b.</span></span> <span data-ttu-id="c4b5a-224">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span> 

    <span data-ttu-id="c4b5a-225">c.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-225">c.</span></span> <span data-ttu-id="c4b5a-226">在 [使用者名稱] 文字方塊中輸入 **Britta Simon**，亦即 Azure 入口網站中的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span></span>

    <span data-ttu-id="c4b5a-227">d.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-227">d.</span></span> <span data-ttu-id="c4b5a-228">在 [密碼] 文字方塊中輸入 Britta 的密碼。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-228">In the **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="c4b5a-229">e.</span><span class="sxs-lookup"><span data-stu-id="c4b5a-229">e.</span></span> <span data-ttu-id="c4b5a-230">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-230">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c4b5a-231">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c4b5a-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c4b5a-232">在本節中，您會將 Halogen Software 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span></span>

![指派使用者][200] 

<span data-ttu-id="c4b5a-234">**若要指派 Britta Simon 到 Halogen Software，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="c4b5a-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b5a-235">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c4b5a-237">在應用程式清單中，選取 [Halogen Software] 。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-237">In the applications list, select **Halogen Software**.</span></span>

    ![設定單一登入](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="c4b5a-239">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-239">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c4b5a-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-241">Click **Add** button.</span></span> <span data-ttu-id="c4b5a-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c4b5a-244">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c4b5a-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4b5a-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4b5a-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c4b5a-247">Testing single sign-on</span></span>

<span data-ttu-id="c4b5a-248">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c4b5a-249">當您在 [存取面板] 中按一下 [Halogen Software] 磚時，您應該會自動登入您的 Halogen Software 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4b5a-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4b5a-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="c4b5a-250">Additional resources</span></span>

* [<span data-ttu-id="c4b5a-251">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="c4b5a-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4b5a-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c4b5a-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
