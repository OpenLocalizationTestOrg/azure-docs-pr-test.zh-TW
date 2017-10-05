---
title: "教學課程：Azure Active Directory 與 Thoughtworks Mingle 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Thoughtworks Mingle 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 268ae5affb88a718f68c08daa94fe7aba4a99c11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="a36f3-103">教學課程：Azure Active Directory 與 Thoughtworks Mingle 整合</span><span class="sxs-lookup"><span data-stu-id="a36f3-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="a36f3-104">在本教學課程中，您將了解如何整合 Thoughtworks Mingle 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a36f3-104">In this tutorial, you learn how to integrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a36f3-105">將 Thoughtworks Mingle 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="a36f3-105">Integrating Thoughtworks Mingle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a36f3-106">您可以在 Azure AD 中控制可存取 Thoughtworks Mingle 的人員</span><span class="sxs-lookup"><span data-stu-id="a36f3-106">You can control in Azure AD who has access to Thoughtworks Mingle</span></span>
- <span data-ttu-id="a36f3-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Thoughtworks Mingle (單一登入)</span><span class="sxs-lookup"><span data-stu-id="a36f3-107">You can enable your users to automatically get signed-on to Thoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a36f3-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="a36f3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a36f3-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a36f3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a36f3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a36f3-110">Prerequisites</span></span>

<span data-ttu-id="a36f3-111">若要設定與 Thoughtworks Mingle 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="a36f3-111">To configure Azure AD integration with Thoughtworks Mingle, you need the following items:</span></span>

- <span data-ttu-id="a36f3-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a36f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a36f3-113">已啟用 Thoughtworks Mingle 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a36f3-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a36f3-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a36f3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a36f3-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a36f3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a36f3-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a36f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a36f3-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a36f3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a36f3-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a36f3-118">Scenario description</span></span>
<span data-ttu-id="a36f3-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a36f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a36f3-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="a36f3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a36f3-121">從資源庫新增 Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="a36f3-121">Adding Thoughtworks Mingle from the gallery</span></span>
2. <span data-ttu-id="a36f3-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a36f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-the-gallery"></a><span data-ttu-id="a36f3-123">從資源庫新增 Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="a36f3-123">Adding Thoughtworks Mingle from the gallery</span></span>
<span data-ttu-id="a36f3-124">若要設定將 Thoughtworks Mingle 整合到 Azure AD 中，您需要從資源庫將 Thoughtworks Mingle 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="a36f3-124">To configure the integration of Thoughtworks Mingle into Azure AD, you need to add Thoughtworks Mingle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a36f3-125">**若要從資源庫新增 Thoughtworks Mingle，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a36f3-125">**To add Thoughtworks Mingle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a36f3-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a36f3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="a36f3-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a36f3-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="a36f3-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a36f3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="a36f3-133">在搜尋方塊中，輸入 **Thoughtworks Mingle**，從結果面板中選取 [Thoughtworks Mingle]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="a36f3-133">In the search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a36f3-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a36f3-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a36f3-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Thoughtworks Mingle 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a36f3-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a36f3-137">若要讓單一登入能夠運作，Azure AD 必須知道 Thoughtworks Mingle 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="a36f3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Thoughtworks Mingle is to a user in Azure AD.</span></span> <span data-ttu-id="a36f3-138">換句話說，必須在 Azure AD 使用者與 Thoughtworks Mingle 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a36f3-138">In other words, a link relationship between an Azure AD user and the related user in Thoughtworks Mingle needs to be established.</span></span>

<span data-ttu-id="a36f3-139">在 Thoughtworks Mingle 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a36f3-139">In Thoughtworks Mingle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a36f3-140">若要搭配 Thoughtworks Mingle 來設定及測試 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="a36f3-140">To configure and test Azure AD single sign-on with Thoughtworks Mingle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a36f3-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="a36f3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a36f3-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a36f3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a36f3-143">**[建立 Thoughtworks Mingle 測試使用者](#create-a-thoughtworks-mingle-test-user)** - 在 Thoughtworks Mingle 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="a36f3-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - to have a counterpart of Britta Simon in Thoughtworks Mingle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a36f3-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a36f3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a36f3-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="a36f3-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a36f3-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a36f3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a36f3-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Thoughtworks Mingle 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a36f3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="a36f3-148">**若要設定透過 Thoughtworks Mingle 使用 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a36f3-148">**To configure Azure AD single sign-on with Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="a36f3-149">在 Azure 入口網站的 [Thoughtworks Mingle] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-149">In the Azure portal, on the **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a36f3-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="a36f3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="a36f3-153">在 [Thoughtworks Mingle 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a36f3-153">On the **Thoughtworks Mingle Domain and URLs** section, perform the following steps:</span></span>

    ![Thoughtworks Mingle 網域和 URL 單一登入資訊](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="a36f3-155">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="a36f3-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a36f3-156">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a36f3-156">The value is not real.</span></span> <span data-ttu-id="a36f3-157">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="a36f3-157">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="a36f3-158">請連絡 [Thoughtworks Mingle 客戶支援小組](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="a36f3-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) to get the value.</span></span> 
 
4. <span data-ttu-id="a36f3-159">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="a36f3-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="a36f3-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a36f3-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a36f3-163">以系統管理員身分登入您的 **Thoughtworks Mingle** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="a36f3-163">Log in to your **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="a36f3-164">按一下 [管理] 索引標籤，然後按一下 [SSO 組態]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-164">Click the **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="a36f3-165">![[管理] 索引標籤](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO 組態")</span><span class="sxs-lookup"><span data-stu-id="a36f3-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="a36f3-166">在 [SSO 組態]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a36f3-166">In the **SSO Config** section, perform the following steps:</span></span>
   
    <span data-ttu-id="a36f3-167">![SSO 組態](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO 組態")</span><span class="sxs-lookup"><span data-stu-id="a36f3-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="a36f3-168">a.</span><span class="sxs-lookup"><span data-stu-id="a36f3-168">a.</span></span> <span data-ttu-id="a36f3-169">若要上傳中繼資料檔案，請按一下 [選擇檔案] 。</span><span class="sxs-lookup"><span data-stu-id="a36f3-169">To upload the metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="a36f3-170">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a36f3-170">b.</span></span> <span data-ttu-id="a36f3-171">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="a36f3-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="a36f3-172">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="a36f3-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a36f3-173">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="a36f3-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a36f3-174">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a36f3-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a36f3-175">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a36f3-175">Create an Azure AD test user</span></span>
<span data-ttu-id="a36f3-176">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a36f3-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="a36f3-178">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a36f3-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a36f3-179">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a36f3-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a36f3-181">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a36f3-183">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a36f3-185">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a36f3-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![[使用者] 對話方塊](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a36f3-187">a.</span><span class="sxs-lookup"><span data-stu-id="a36f3-187">a.</span></span> <span data-ttu-id="a36f3-188">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a36f3-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a36f3-189">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a36f3-189">b.</span></span> <span data-ttu-id="a36f3-190">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="a36f3-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a36f3-191">c.</span><span class="sxs-lookup"><span data-stu-id="a36f3-191">c.</span></span> <span data-ttu-id="a36f3-192">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="a36f3-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a36f3-193">d.</span><span class="sxs-lookup"><span data-stu-id="a36f3-193">d.</span></span> <span data-ttu-id="a36f3-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a36f3-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="a36f3-195">建立 Thoughtworks Mingle 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a36f3-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="a36f3-196">若要讓 Azure AD 使用者能夠登入，必須使用他們的 Azure Active Directory 使用者名稱將他們佈建到 Thoughtworks Mingle 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a36f3-196">For Azure AD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="a36f3-197">Thoughtworks Mingle 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="a36f3-197">In the case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="a36f3-198">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a36f3-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="a36f3-199">以系統管理員身分登入您的 Thoughtworks Mingle 公司網站。</span><span class="sxs-lookup"><span data-stu-id="a36f3-199">Log in to your Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="a36f3-200">按一下 [設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="a36f3-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="a36f3-201">![第一個專案](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "第一個專案")</span><span class="sxs-lookup"><span data-stu-id="a36f3-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="a36f3-202">按一下 [管理] 索引標籤，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-202">Click the **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="a36f3-203">![使用者](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="a36f3-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="a36f3-204">按一下 [新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="a36f3-204">Click **New User**.</span></span>
   
    <span data-ttu-id="a36f3-205">![新增使用者](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="a36f3-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="a36f3-206">在 [新增使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a36f3-206">On the **New User** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="a36f3-207">![[新增使用者] 對話方塊](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "[新增使用者]")</span><span class="sxs-lookup"><span data-stu-id="a36f3-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="a36f3-208">a.</span><span class="sxs-lookup"><span data-stu-id="a36f3-208">a.</span></span> <span data-ttu-id="a36f3-209">在相關的文字方塊中，輸入您要佈建之有效 Azure AD 帳戶的 [登入名稱]、[顯示名稱]、[選擇密碼]、[確認密碼]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-209">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="a36f3-210">b.</span><span class="sxs-lookup"><span data-stu-id="a36f3-210">b.</span></span> <span data-ttu-id="a36f3-211">選取 [完整使用者] 做為 [使用者類型]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="a36f3-212">c.</span><span class="sxs-lookup"><span data-stu-id="a36f3-212">c.</span></span> <span data-ttu-id="a36f3-213">按一下 [建立這個設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="a36f3-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="a36f3-214">您可以使用任何其他的 Thoughtworks Mingle 使用者帳戶建立工具或 Thoughtworks Mingle 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a36f3-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a36f3-215">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a36f3-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="a36f3-216">在本節中，您會將 Thoughtworks Mingle 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a36f3-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Thoughtworks Mingle.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="a36f3-218">**若要將 Britta Simon 指派給 Thoughtworks Mingle，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a36f3-218">**To assign Britta Simon to Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="a36f3-219">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a36f3-221">在應用程式清單中，選取 [Thoughtworks Mingle]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-221">In the applications list, select **Thoughtworks Mingle**.</span></span>

    ![應用程式清單中的 [Thoughtworks Mingle] 連結](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="a36f3-223">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-223">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202] 

4. <span data-ttu-id="a36f3-225">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a36f3-225">Click **Add** button.</span></span> <span data-ttu-id="a36f3-226">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="a36f3-228">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="a36f3-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a36f3-229">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a36f3-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a36f3-230">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a36f3-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a36f3-231">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a36f3-231">Test single sign-on</span></span>

<span data-ttu-id="a36f3-232">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="a36f3-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a36f3-233">當您在「存取面板」中按一下 [Thoughtworks Mingle] 圖格時，應該會自動登入您的 Thoughtworks Mingle 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a36f3-233">When you click the Thoughtworks Mingle tile in the Access Panel, you should get automatically signed-on to your Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a36f3-234">其他資源</span><span class="sxs-lookup"><span data-stu-id="a36f3-234">Additional resources</span></span>

* [<span data-ttu-id="a36f3-235">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="a36f3-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a36f3-236">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a36f3-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

