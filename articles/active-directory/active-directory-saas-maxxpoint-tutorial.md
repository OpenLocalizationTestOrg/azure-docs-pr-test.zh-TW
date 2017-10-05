---
title: "教學課程：Azure Active Directory 與 MaxxPoint 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 MaxxPoint 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 8a7481b71df5ca407dbed5da3d3cc26991504c82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="7d770-103">教學課程：Azure Active Directory 與 MaxxPoint 整合</span><span class="sxs-lookup"><span data-stu-id="7d770-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="7d770-104">在本教學課程中，您會了解如何將 MaxxPoint 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="7d770-104">In this tutorial, you learn how to integrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d770-105">將 MaxxPoint 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7d770-105">Integrating MaxxPoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7d770-106">您可以在 Azure AD 中控制可存取 MaxxPoint 的人員</span><span class="sxs-lookup"><span data-stu-id="7d770-106">You can control in Azure AD who has access to MaxxPoint</span></span>
- <span data-ttu-id="7d770-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 MaxxPoint (單一登入)</span><span class="sxs-lookup"><span data-stu-id="7d770-107">You can enable your users to automatically get signed-on to MaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d770-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="7d770-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7d770-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7d770-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d770-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7d770-110">Prerequisites</span></span>

<span data-ttu-id="7d770-111">若要設定 Azure AD 與 MaxxPoint 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7d770-111">To configure Azure AD integration with MaxxPoint, you need the following items:</span></span>

- <span data-ttu-id="7d770-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7d770-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d770-113">已啟用 MaxxPoint 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7d770-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d770-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7d770-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d770-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7d770-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d770-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="7d770-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7d770-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7d770-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d770-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7d770-118">Scenario description</span></span>
<span data-ttu-id="7d770-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d770-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d770-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7d770-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d770-121">從資源庫新增 MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="7d770-121">Adding MaxxPoint from the gallery</span></span>
2. <span data-ttu-id="7d770-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7d770-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-the-gallery"></a><span data-ttu-id="7d770-123">從資源庫新增 MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="7d770-123">Adding MaxxPoint from the gallery</span></span>
<span data-ttu-id="7d770-124">若要設定將 MaxxPoint 整合到 Azure AD 中，您需要從資源庫將 MaxxPoint 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="7d770-124">To configure the integration of MaxxPoint into Azure AD, you need to add MaxxPoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7d770-125">**若要從資源庫加入 MaxxPoint，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d770-125">**To add MaxxPoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7d770-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7d770-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7d770-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7d770-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7d770-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7d770-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7d770-131">按一下對話方塊頂端的 [新應用程式] 按鈕來新增新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d770-131">Click **New application** button on the top of dialog to add new application.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7d770-133">在搜尋方塊中，輸入 **MaxxPoint**。</span><span class="sxs-lookup"><span data-stu-id="7d770-133">In the search box, type **MaxxPoint**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="7d770-135">在結果窗格中，選取 [MaxxPoint]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d770-135">In the results panel, select **MaxxPoint**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7d770-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7d770-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7d770-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 MaxxPoint 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d770-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7d770-139">若要讓單一登入能夠運作，Azure AD 必須知道 MaxxPoint 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7d770-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MaxxPoint is to a user in Azure AD.</span></span> <span data-ttu-id="7d770-140">換句話說，必須在 Azure AD 使用者和 MaxxPoint 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7d770-140">In other words, a link relationship between an Azure AD user and the related user in MaxxPoint needs to be established.</span></span>

<span data-ttu-id="7d770-141">建立此連結關聯性的方法，就是指派 Azure AD 中**使用者名稱**的值做為 MaxxPoint 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="7d770-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MaxxPoint.</span></span>

<span data-ttu-id="7d770-142">若要使用 MaxxPoint 設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7d770-142">To configure and test Azure AD single sign-on with MaxxPoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7d770-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7d770-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7d770-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d770-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d770-145">**[建立 MaxxPoint 測試使用者](#creating-a-maxxpoint-test-user)** - 使 MaxxPoint 中 Britta Simon 的對應使用者能夠連結到代表她在 Azure AD 中的項目。</span><span class="sxs-lookup"><span data-stu-id="7d770-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - to have a counterpart of Britta Simon in MaxxPoint that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7d770-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d770-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d770-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7d770-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7d770-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7d770-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7d770-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 MaxxPoint 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d770-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="7d770-150">**若要使用 MaxxPoint 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d770-150">**To configure Azure AD single sign-on with MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="7d770-151">在 Azure 入口網站的 [MaxxPoint] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7d770-151">In the Azure portal, on the **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7d770-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d770-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="7d770-155">在 [MaxxPoint 網域和 URL] 區段中，如果您想要在 [IDP 起始模式] 中設定應用程式，則不需要執行任何步驟。</span><span class="sxs-lookup"><span data-stu-id="7d770-155">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, no need to perform any steps.</span></span>

    ![設定單一登入](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="7d770-157">在 [MaxxPoint 網域和 URL] 區段中，如果您想要在 [SP 起始模式] 中設定應用程式，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7d770-157">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="7d770-159">a.</span><span class="sxs-lookup"><span data-stu-id="7d770-159">a.</span></span> <span data-ttu-id="7d770-160">按一下 [顯示進階 URL 設定] 選項。</span><span class="sxs-lookup"><span data-stu-id="7d770-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="7d770-161">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d770-161">b.</span></span> <span data-ttu-id="7d770-162">在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="7d770-162">In the **Sign On URL** textbox, type a URL using the following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7d770-163">請注意，這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7d770-163">Please note that this is not the real value.</span></span> <span data-ttu-id="7d770-164">您必須使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="7d770-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="7d770-165">請撥打電話 (**888-728-0950**) 給 MaxxPoint 小組以取得這個值。</span><span class="sxs-lookup"><span data-stu-id="7d770-165">Call MaxxPoint team on **888-728-0950** to get this value.</span></span>

5. <span data-ttu-id="7d770-166">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7d770-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="7d770-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d770-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7d770-170">若要為您的應用程式設定 SSO，請撥打電話 (**888-728-0950**) 給 MaxxPoint 支援小組，他們將會進一步協助您將所下載的「中繼資料 XML」檔案提供給他們。</span><span class="sxs-lookup"><span data-stu-id="7d770-170">To get SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how to provide them the downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="7d770-171">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7d770-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7d770-172">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7d770-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7d770-173">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7d770-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7d770-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7d770-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="7d770-175">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7d770-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7d770-177">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d770-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7d770-178">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7d770-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7d770-180">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="7d770-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7d770-182">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7d770-182">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d770-184">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7d770-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7d770-186">a.</span><span class="sxs-lookup"><span data-stu-id="7d770-186">a.</span></span> <span data-ttu-id="7d770-187">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7d770-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d770-188">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d770-188">b.</span></span> <span data-ttu-id="7d770-189">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7d770-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7d770-190">c.</span><span class="sxs-lookup"><span data-stu-id="7d770-190">c.</span></span> <span data-ttu-id="7d770-191">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="7d770-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7d770-192">d.</span><span class="sxs-lookup"><span data-stu-id="7d770-192">d.</span></span> <span data-ttu-id="7d770-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7d770-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="7d770-194">建立 MaxxPoint 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7d770-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="7d770-195">在本節中，您要在 MaxxPoint 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="7d770-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="7d770-196">請撥打電話 (**888-728-0950**) 給 MaxxPoint 支援小組，以在 MaxxPoint 應用程式中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="7d770-196">Please call MaxxPoint support team on **888-728-0950** to add the users in the MaxxPoint application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7d770-197">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7d770-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7d770-198">在本節中，您會將 MaxxPoint 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d770-198">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to MaxxPoint.</span></span>

![指派使用者][200] 

<span data-ttu-id="7d770-200">**若要將 Britta Simon 指派到 MaxxPoint，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d770-200">**To assign Britta Simon to MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="7d770-201">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7d770-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7d770-203">在應用程式清單中，選取 [MaxxPoint]。</span><span class="sxs-lookup"><span data-stu-id="7d770-203">In the applications list, select **MaxxPoint**.</span></span>

    ![設定單一登入](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="7d770-205">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7d770-205">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7d770-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d770-207">Click **Add** button.</span></span> <span data-ttu-id="7d770-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7d770-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7d770-210">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7d770-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7d770-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d770-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d770-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d770-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7d770-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7d770-213">Testing single sign-on</span></span>

<span data-ttu-id="7d770-214">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="7d770-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7d770-215">當您在存取面板中按一下 [MaxxPoint] 圖格時，應該會自動登入您的 MaxxPoint 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d770-215">When you click the MaxxPoint tile in the Access Panel, you should get automatically signed-on to your MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7d770-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="7d770-216">Additional resources</span></span>

* [<span data-ttu-id="7d770-217">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7d770-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d770-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7d770-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png