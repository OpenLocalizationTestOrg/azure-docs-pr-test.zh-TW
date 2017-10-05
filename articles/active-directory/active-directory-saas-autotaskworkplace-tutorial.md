---
title: "教學課程：Azure Active Directory 與 Autotask Workplace 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Autotask Workplace 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 45130162271b20860607497ff93c6a668c415233
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="be443-103">教學課程：Azure Active Directory 與 Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="be443-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="be443-104">在本教學課程中，您會了解如何將 Autotask Workplace 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="be443-104">In this tutorial, you learn how to integrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="be443-105">將 Autotask Workplace 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="be443-105">Integrating Autotask Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="be443-106">您可以在 Azure AD 中控制可存取 Autotask Workplace 的人員</span><span class="sxs-lookup"><span data-stu-id="be443-106">You can control in Azure AD who has access to Autotask Workplace</span></span>
- <span data-ttu-id="be443-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Autotask Workplace (單一登入)</span><span class="sxs-lookup"><span data-stu-id="be443-107">You can enable your users to automatically get signed-on to Autotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="be443-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="be443-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="be443-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="be443-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be443-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="be443-110">Prerequisites</span></span>

<span data-ttu-id="be443-111">若要設定 Azure AD 與 Autotask Workplace 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="be443-111">To configure Azure AD integration with Autotask Workplace, you need the following items:</span></span>

- <span data-ttu-id="be443-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="be443-112">An Azure AD subscription</span></span>
- <span data-ttu-id="be443-113">已啟用 Autotask Workplace 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="be443-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="be443-114">您必須是工作地點的系統管理員或進階系統管理員。</span><span class="sxs-lookup"><span data-stu-id="be443-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="be443-115">您必須擁有 Azure AD 的 Administrator 帳戶。</span><span class="sxs-lookup"><span data-stu-id="be443-115">You must have an administrator account in the Azure AD.</span></span>
- <span data-ttu-id="be443-116">利用這項功能的使用者必須有 Workplace 和 Azure AD 內的帳戶，而且兩者的電子郵件地址必須相符。</span><span class="sxs-lookup"><span data-stu-id="be443-116">The users that will utilize this feature must have accounts within Workplace and the Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="be443-117">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="be443-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="be443-118">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="be443-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="be443-119">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="be443-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="be443-120">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="be443-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="be443-121">案例描述</span><span class="sxs-lookup"><span data-stu-id="be443-121">Scenario description</span></span>
<span data-ttu-id="be443-122">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="be443-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="be443-123">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="be443-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="be443-124">從資源庫新增 Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="be443-124">Adding Autotask Workplace from the gallery</span></span>
2. <span data-ttu-id="be443-125">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="be443-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-the-gallery"></a><span data-ttu-id="be443-126">從資源庫新增 Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="be443-126">Adding Autotask Workplace from the gallery</span></span>
<span data-ttu-id="be443-127">若要設定將 Autotask Workplace 整合到 Azure AD 中，您需要從資源庫將 Autotask Workplace 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="be443-127">To configure the integration of Autotask Workplace into Azure AD, you need to add Autotask Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="be443-128">**若要從資源庫新增 Autotask Workplace，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="be443-128">**To add Autotask Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="be443-129">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="be443-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="be443-131">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="be443-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="be443-132">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="be443-132">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="be443-134">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be443-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="be443-136">在搜尋方塊中，輸入 **Autotask Workplace**，從結果面板中選取 [Autotask Workplace]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="be443-136">In the search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button to add the application.</span></span>

    ![在結果清單中的 Autotask Workplace](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="be443-138">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="be443-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="be443-139">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Autotask Workplace 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="be443-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="be443-140">若要讓單一登入能夠運作，Azure AD 必須知道 Autotask Workplace 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="be443-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Autotask Workplace is to a user in Azure AD.</span></span> <span data-ttu-id="be443-141">換句話說，必須在 Azure AD 使用者與 Autotask Workplace 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="be443-141">In other words, a link relationship between an Azure AD user and the related user in Autotask Workplace needs to be established.</span></span>

<span data-ttu-id="be443-142">在 Autotask Workplace 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="be443-142">In Autotask Workplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="be443-143">若要設定及測試與 Autotask Workplace 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="be443-143">To configure and test Azure AD single sign-on with Autotask Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="be443-144">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="be443-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="be443-145">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="be443-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="be443-146">**[建立 Autotask Workplace 測試使用者](#create-an-autotask-workplace-test-user)** - 在 Autotask Workplace 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="be443-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - to have a counterpart of Britta Simon in Autotask Workplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="be443-147">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="be443-147">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="be443-148">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="be443-148">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="be443-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="be443-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="be443-150">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Autotask Workplace 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="be443-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="be443-151">**若要設定與 Autotask Workplace 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="be443-151">**To configure Azure AD single sign-on with Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="be443-152">在 Azure 入口網站的 [Autotask Workplace] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="be443-152">In the Azure portal, on the **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="be443-154">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="be443-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="be443-156">如果您想要以 **IDP** 起始模式設定應用程式，請在 [Autotask Workplace 網域及 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="be443-156">If you wish to configure the application in **IDP** initiated mode, perform the following steps on the **Autotask Workplace Domain and URLs** section:</span></span>

    ![IDP 的 Autotask Workplace 網域和 URL 單一登入資訊](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="be443-158">a.</span><span class="sxs-lookup"><span data-stu-id="be443-158">a.</span></span> <span data-ttu-id="be443-159">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="be443-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="be443-160">b.</span><span class="sxs-lookup"><span data-stu-id="be443-160">b.</span></span> <span data-ttu-id="be443-161">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="be443-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="be443-162">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="be443-162">If you wish to configure the application in **SP** initiated mode, check **Show advanced URL settings** and perform the following steps:</span></span>

    ![SP 的 Autotask Workplace 網域和 URL 單一登入資訊](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="be443-164">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="be443-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="be443-165">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="be443-165">These values are not real.</span></span> <span data-ttu-id="be443-166">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="be443-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="be443-167">請連絡 [Autotask Workplace 用戶端支援小組](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="be443-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get these values.</span></span> 

5. <span data-ttu-id="be443-168">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="be443-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="be443-170">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="be443-170">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="be443-172">在不同的網頁瀏覽器視窗中，使用系統管理員認證登入 Workplace Online。</span><span class="sxs-lookup"><span data-stu-id="be443-172">In a different web browser window, Log in to Workplace Online using the administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="be443-173">設定 IdP 時，需要指定子網域。</span><span class="sxs-lookup"><span data-stu-id="be443-173">When configuring the IdP, a subdomain will need to be specified.</span></span> <span data-ttu-id="be443-174">若要確認正確的子網域，請登入 Workplace Online。</span><span class="sxs-lookup"><span data-stu-id="be443-174">To confirm the correct subdomain, login to Workplace Online.</span></span> <span data-ttu-id="be443-175">登入後，記下 URL 中的子網域。</span><span class="sxs-lookup"><span data-stu-id="be443-175">Once logged in, make note to the subdomain in the URL.</span></span>
    ><span data-ttu-id="be443-176">子網域是 “https://“ 和 “.awp.autotask.net/“ 之間的部分，而且應該是 us、eu、ca 或 au。</span><span class="sxs-lookup"><span data-stu-id="be443-176">The subdomain is the part between the “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="be443-177">移至 [組態] > [單一登入]，並執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="be443-177">Go to **Configuration** > **Single Sign-On** and perform the following steps:</span></span>

    ![Autotask 單一登入組態](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="be443-179">a.</span><span class="sxs-lookup"><span data-stu-id="be443-179">a.</span></span> <span data-ttu-id="be443-180">選取 [XML 中繼資料檔案] 選項，然後上傳從 Azure 入口網站下載的 [中繼資料 XML]。</span><span class="sxs-lookup"><span data-stu-id="be443-180">Select the **XML Metadata File** option, and then upload the **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="be443-181">b.</span><span class="sxs-lookup"><span data-stu-id="be443-181">b.</span></span> <span data-ttu-id="be443-182">按一下 [啟用 SSO]。</span><span class="sxs-lookup"><span data-stu-id="be443-182">Click **Enable SSO**.</span></span>
    
    ![Autotask 單一登入核准組態](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="be443-184">c.</span><span class="sxs-lookup"><span data-stu-id="be443-184">c.</span></span> <span data-ttu-id="be443-185">選取 [我確認這項資訊正確，而且我信任此 IdP] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="be443-185">Select the **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="be443-186">d.</span><span class="sxs-lookup"><span data-stu-id="be443-186">d.</span></span> <span data-ttu-id="be443-187">按一下 [核准]。</span><span class="sxs-lookup"><span data-stu-id="be443-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="be443-188">如果您需要協助設定 Autotask Workplace，請參閱[本頁](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)取得 Workplace 帳戶的協助。</span><span class="sxs-lookup"><span data-stu-id="be443-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="be443-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="be443-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="be443-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="be443-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="be443-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="be443-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="be443-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="be443-192">Create an Azure AD test user</span></span>

<span data-ttu-id="be443-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="be443-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="be443-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="be443-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="be443-196">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be443-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="be443-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="be443-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="be443-200">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="be443-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="be443-202">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="be443-202">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="be443-204">a.</span><span class="sxs-lookup"><span data-stu-id="be443-204">a.</span></span> <span data-ttu-id="be443-205">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="be443-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="be443-206">b.</span><span class="sxs-lookup"><span data-stu-id="be443-206">b.</span></span> <span data-ttu-id="be443-207">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="be443-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="be443-208">c.</span><span class="sxs-lookup"><span data-stu-id="be443-208">c.</span></span> <span data-ttu-id="be443-209">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="be443-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="be443-210">d.</span><span class="sxs-lookup"><span data-stu-id="be443-210">d.</span></span> <span data-ttu-id="be443-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="be443-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="be443-212">建立 Autotask Workplace 測試使用者</span><span class="sxs-lookup"><span data-stu-id="be443-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="be443-213">在本節中，您會在 Autotask 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="be443-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="be443-214">請與 [Autotask Workplace 支援小組](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)合作，在 Autotask Workplace 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="be443-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to add the users in the Autotask Workplace platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="be443-215">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="be443-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="be443-216">在本節中，您會將 Autotask Workplace 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="be443-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Autotask Workplace.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="be443-218">**若要將 Britta Simon 指派給 Autotask Workplace，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="be443-218">**To assign Britta Simon to Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="be443-219">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="be443-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="be443-221">在應用程式清單中，選取 [Autotask Workplace]。</span><span class="sxs-lookup"><span data-stu-id="be443-221">In the applications list, select **Autotask Workplace**.</span></span>

    ![應用程式清單中的 Autotask Workplace 連結](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="be443-223">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="be443-223">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="be443-225">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be443-225">Click **Add** button.</span></span> <span data-ttu-id="be443-226">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="be443-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="be443-228">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="be443-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="be443-229">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be443-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="be443-230">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be443-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="be443-231">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="be443-231">Test single sign-on</span></span>

<span data-ttu-id="be443-232">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="be443-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="be443-233">當您在「存取面板」中按一下 [Autotask Workplace] 圖格時，應該會自動登入您的 Autotask Workplace 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be443-233">When you click the Autotask Workplace tile in the Access Panel, you should get automatically signed-on to your Autotask Workplace application.</span></span>
<span data-ttu-id="be443-234">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="be443-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="be443-235">其他資源</span><span class="sxs-lookup"><span data-stu-id="be443-235">Additional resources</span></span>

* [<span data-ttu-id="be443-236">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="be443-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be443-237">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="be443-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

