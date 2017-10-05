---
title: "教學課程：Azure Active Directory 與 Evidence.com 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Evidence.com 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: a9c474cfc648fc8a306d736c89a4813d82c133ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="039ca-103">教學課程：Azure Active Directory 與 Evidence.com 整合</span><span class="sxs-lookup"><span data-stu-id="039ca-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="039ca-104">在本教學課程中，您將了解如何整合 Evidence.com 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="039ca-104">In this tutorial, you learn how to integrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="039ca-105">Evidence.com 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="039ca-105">Integrating Evidence.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="039ca-106">您可以在 Azure AD 中管控可存取 Evidence.com 的人員。</span><span class="sxs-lookup"><span data-stu-id="039ca-106">You can control in Azure AD who has access to Evidence.com.</span></span>
- <span data-ttu-id="039ca-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 Evidence.com (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="039ca-107">You can enable your users to automatically get signed-on to Evidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="039ca-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="039ca-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="039ca-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="039ca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="039ca-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="039ca-110">Prerequisites</span></span>

<span data-ttu-id="039ca-111">若要設定 Azure AD 與 Evidence.com 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="039ca-111">To configure Azure AD integration with Evidence.com, you need the following items:</span></span>

- <span data-ttu-id="039ca-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="039ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="039ca-113">已啟用 Evidence.com 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="039ca-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="039ca-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="039ca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="039ca-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="039ca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="039ca-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="039ca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="039ca-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="039ca-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="039ca-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="039ca-118">Scenario description</span></span>
<span data-ttu-id="039ca-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="039ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="039ca-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="039ca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="039ca-121">從資源庫新增 Evidence.com</span><span class="sxs-lookup"><span data-stu-id="039ca-121">Adding Evidence.com from the gallery</span></span>
2. <span data-ttu-id="039ca-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="039ca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-the-gallery"></a><span data-ttu-id="039ca-123">從資源庫新增 Evidence.com</span><span class="sxs-lookup"><span data-stu-id="039ca-123">Adding Evidence.com from the gallery</span></span>
<span data-ttu-id="039ca-124">若要設定將 Evidence.com 整合到 Azure AD 中，您需要從資源庫將 Evidence.com 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="039ca-124">To configure the integration of Evidence.com into Azure AD, you need to add Evidence.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="039ca-125">**若要從資源庫新增 Evidence.com，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="039ca-125">**To add Evidence.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="039ca-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="039ca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="039ca-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="039ca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="039ca-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="039ca-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="039ca-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="039ca-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="039ca-133">在搜尋方塊中，輸入 **Evidence.com**，從結果面板中選取 [Evidence.com]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="039ca-133">In the search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="039ca-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="039ca-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="039ca-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Evidence.com 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="039ca-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="039ca-137">若要讓單一登入能夠運作，Azure AD 必須知道 Evidence.com 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="039ca-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evidence.com is to a user in Azure AD.</span></span> <span data-ttu-id="039ca-138">換句話說，必須在 Azure AD 使用者和 Evidence.com 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="039ca-138">In other words, a link relationship between an Azure AD user and the related user in Evidence.com needs to be established.</span></span>

<span data-ttu-id="039ca-139">在 Evidence.com 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="039ca-139">In Evidence.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="039ca-140">若要設定並測試透過 Evidence.com 使用 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="039ca-140">To configure and test Azure AD single sign-on with Evidence.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="039ca-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="039ca-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="039ca-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="039ca-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="039ca-143">**[建立 Evidence.com 測試使用者](#create-a-evidencecom-test-user)** - 使 Evidence.com 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="039ca-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - to have a counterpart of Britta Simon in Evidence.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="039ca-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="039ca-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="039ca-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="039ca-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="039ca-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="039ca-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="039ca-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Evidence.com 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="039ca-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="039ca-148">**若要設定透過 Evidence.com 使用 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="039ca-148">**To configure Azure AD single sign-on with Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="039ca-149">在 Azure 入口網站的 [Evidence.com] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="039ca-149">In the Azure portal, on the **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="039ca-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="039ca-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="039ca-153">在 [Evidence.com 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="039ca-153">On the **Evidence.com Domain and URLs** section, perform the following steps:</span></span>

    ![Evidence.com 網域及 URL 單一登入資訊](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="039ca-155">a.</span><span class="sxs-lookup"><span data-stu-id="039ca-155">a.</span></span> <span data-ttu-id="039ca-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="039ca-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="039ca-157">b.</span><span class="sxs-lookup"><span data-stu-id="039ca-157">b.</span></span> <span data-ttu-id="039ca-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="039ca-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="039ca-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="039ca-159">These values are not real.</span></span> <span data-ttu-id="039ca-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="039ca-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="039ca-161">請連絡 [Evidence.com 用戶端支援小組](https://communities.taser.com/support/SupportContactUs?typ=LE)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="039ca-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) to get these values.</span></span> 

4. <span data-ttu-id="039ca-162">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="039ca-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="039ca-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="039ca-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="039ca-166">在 [Evidence.com 組態] 區段上，按一下 [設定 Evidence.com] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="039ca-166">On the **Evidence.com Configuration** section, click **Configure Evidence.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="039ca-167">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="039ca-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Evidence.com 設定](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="039ca-169">在個別的網頁瀏覽器視窗中，以系統管理員身分登入您的 Evidence.com 租用戶，並瀏覽至 [Admin]  索引標籤</span><span class="sxs-lookup"><span data-stu-id="039ca-169">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span></span>

8. <span data-ttu-id="039ca-170">按一下 [機構單一登入] </span><span class="sxs-lookup"><span data-stu-id="039ca-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="039ca-171">選取 [SAML 型單一登入] </span><span class="sxs-lookup"><span data-stu-id="039ca-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="039ca-172">將顯示在 Azure 入口網站中的 **SAML 實體 ID**、**SAML 單一登入服務 URL** 和**登出 URL** 值複製到 Evidence.com 中的對應欄位。</span><span class="sxs-lookup"><span data-stu-id="039ca-172">Copy the **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in the Azure portal and to the corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="039ca-173">在記事本中開啟您下載的憑證 (Base64) 檔案，將其內容複製到剪貼簿，然後貼到 [安全性憑證] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="039ca-173">Open your downloaded Certificate(Base64) file in notepad, copy the content of it into your clipboard, and then paste it to the **Security Certificate** box.</span></span> 

12. <span data-ttu-id="039ca-174">在 Evidence.com 中儲存組態。</span><span class="sxs-lookup"><span data-stu-id="039ca-174">Save the configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="039ca-175">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="039ca-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="039ca-176">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="039ca-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="039ca-177">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="039ca-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="039ca-178">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="039ca-178">Create an Azure AD test user</span></span>

<span data-ttu-id="039ca-179">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="039ca-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="039ca-181">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="039ca-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="039ca-182">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="039ca-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="039ca-184">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="039ca-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="039ca-186">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="039ca-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="039ca-188">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="039ca-188">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="039ca-190">a.</span><span class="sxs-lookup"><span data-stu-id="039ca-190">a.</span></span> <span data-ttu-id="039ca-191">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="039ca-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="039ca-192">b.</span><span class="sxs-lookup"><span data-stu-id="039ca-192">b.</span></span> <span data-ttu-id="039ca-193">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="039ca-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="039ca-194">c.</span><span class="sxs-lookup"><span data-stu-id="039ca-194">c.</span></span> <span data-ttu-id="039ca-195">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="039ca-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="039ca-196">d.</span><span class="sxs-lookup"><span data-stu-id="039ca-196">d.</span></span> <span data-ttu-id="039ca-197">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="039ca-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="039ca-198">建立 Evidence.com 測試使用者</span><span class="sxs-lookup"><span data-stu-id="039ca-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="039ca-199">必須先針對 Evidence.com 應用程式內的存取佈建 Azure AD 使用者，才可以讓他們登入。</span><span class="sxs-lookup"><span data-stu-id="039ca-199">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span></span> <span data-ttu-id="039ca-200">本節描述如何建立 Evidence.com 內的 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="039ca-200">This section describes how to create Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="039ca-201">**若要在 Evidence.com 中佈建使用者帳戶：**</span><span class="sxs-lookup"><span data-stu-id="039ca-201">**To provision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="039ca-202">在網頁瀏覽器視窗中，以系統管理員身分登入您的 Evidence.com 公司網站。</span><span class="sxs-lookup"><span data-stu-id="039ca-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="039ca-203">瀏覽至 [Admin]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="039ca-203">Navigate to **Admin** tab.</span></span>

3. <span data-ttu-id="039ca-204">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="039ca-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="039ca-205">按一下 [新增]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="039ca-205">Click the **Add** button.</span></span>

5. <span data-ttu-id="039ca-206">所新增之使用者的 [電子郵件地址]  必須符合 Azure AD 中想要允許存取的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="039ca-206">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span></span> <span data-ttu-id="039ca-207">如果使用者名稱和電子郵件地址不是您組織中的相同值，您可以使用 Azure 入口網站的 **[Evidence.com] > [屬性] > [單一登入]** 區段，將傳送至 Evidence.com 的 nameidenitifer 變更為電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="039ca-207">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure portal to change the nameidenitifer sent to Evidence.com to be the email address.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="039ca-208">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="039ca-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="039ca-209">在本節中，您會將 Evidence.com 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="039ca-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evidence.com.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="039ca-211">**若要將 Britta Simon 指派到 Evidence.com，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="039ca-211">**To assign Britta Simon to Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="039ca-212">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="039ca-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="039ca-214">在應用程式清單中，選取 [Evidence.com]。</span><span class="sxs-lookup"><span data-stu-id="039ca-214">In the applications list, select **Evidence.com**.</span></span>

    ![應用程式清單中的 Evidence.com 連結](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="039ca-216">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="039ca-216">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="039ca-218">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="039ca-218">Click **Add** button.</span></span> <span data-ttu-id="039ca-219">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="039ca-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="039ca-221">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="039ca-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="039ca-222">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="039ca-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="039ca-223">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="039ca-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="039ca-224">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="039ca-224">Test single sign-on</span></span>

<span data-ttu-id="039ca-225">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="039ca-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="039ca-226">在「存取面板」中按一下 Evidence.com 圖格時，應該會自動登入 Evidence.com 應用程式。</span><span class="sxs-lookup"><span data-stu-id="039ca-226">When you click the Evidence.com tile in the Access Panel, you should get automatically signed-on to your Evidence.com application.</span></span>
<span data-ttu-id="039ca-227">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="039ca-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="039ca-228">其他資源</span><span class="sxs-lookup"><span data-stu-id="039ca-228">Additional resources</span></span>

* [<span data-ttu-id="039ca-229">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="039ca-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="039ca-230">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="039ca-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

