---
title: "使用 Azure Active Directory 授權開發人員帳戶 - Azure API 管理 | Microsoft Docs"
description: "了解如何在 API 管理中使用 Azure Active Directory 授權使用者"
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7637e6419d17a2d75904fbe63df5f27d4be4bbe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="83224-103">如何在 Azure API 管理中使用 Azure Active Directory 授權開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="83224-103">How to authorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="83224-104">概觀</span><span class="sxs-lookup"><span data-stu-id="83224-104">Overview</span></span>
<span data-ttu-id="83224-105">本指南說明如何讓使用者能夠從 Azure Active Directory 存取開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="83224-105">This guide shows you how to enable access to the developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="83224-106">本指南也說明如何管理 Azure Active Directory 的使用者，方法是加入包含 Azure Active Directory 的使用者的外部群組。</span><span class="sxs-lookup"><span data-stu-id="83224-106">This guide also shows you how to manage groups of Azure Active Directory users by adding external groups that contain the users of an Azure Active Directory.</span></span>

> <span data-ttu-id="83224-107">若要完成本指南中的步驟，您必須先具備要在其中建立應用程式的 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="83224-107">To complete the steps in this guide you must first have an Azure Active Directory in which to create an application.</span></span>
> 
> 

## <a name="how-to-authorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="83224-108">如何使用 Azure Active Directory 授權開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="83224-108">How to authorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="83224-109">若要開始，請在 API 管理服務的 Azure 入口網站中按一下 [發佈者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="83224-109">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="83224-110">這會帶您前往 API 管理發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="83224-110">This takes you to the API Management publisher portal.</span></span>

![發行者入口網站][api-management-management-console]

> <span data-ttu-id="83224-112">如果您尚未建立 API 管理服務執行個體，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]教學課程中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="83224-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="83224-113">從左側的 [API 管理] 功能表按一下 [安全性]，然後按一下 [外部身分識別]。</span><span class="sxs-lookup"><span data-stu-id="83224-113">Click **Security** from the **API Management** menu on the left and click **External Identities**.</span></span>

![外部身分識別][api-management-security-external-identities]

<span data-ttu-id="83224-115">按一下 [ **Azure Active Directory**]。</span><span class="sxs-lookup"><span data-stu-id="83224-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="83224-116">記下 [重新導向 URL]  ，然後切換到 Azure 傳統入口網站中您的 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="83224-116">Make a note of the **Redirect URL** and switch over to your Azure Active Directory in the Azure Classic Portal.</span></span>

![外部身分識別][api-management-security-aad-new]

<span data-ttu-id="83224-118">按一下 [新增] 按鈕來建立新 Azure Active Directory 應用程式，並選擇 [新增我的組織正在開發的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="83224-118">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![加入新的 Azure Active Directory 應用程式][api-management-new-aad-application-menu]

<span data-ttu-id="83224-120">輸入應用程式的名稱，選取 [ **Web 應用程式和/或 Web API**]，然後按 [下一步] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="83224-120">Enter a name for the application, select **Web application and/or Web API**, and click the next button.</span></span>

![新 Azure Active Directory 應用程式][api-management-new-aad-application-1]

<span data-ttu-id="83224-122">在 [登入 URL] 中，輸入開發人員入口網站的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="83224-122">For **Sign-on URL**, enter the sign-on URL of your developer portal.</span></span> <span data-ttu-id="83224-123">在此範例中，[登入 URL] 為 `https://aad03.portal.current.int-azure-api.net/signin`。</span><span class="sxs-lookup"><span data-stu-id="83224-123">In this example, the **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="83224-124">針對 [ **應用程式識別碼 URL**]，請輸入 Azure Active Directory 的預設網域或自訂網域，並為其附加獨特的字串。</span><span class="sxs-lookup"><span data-stu-id="83224-124">For the **App ID URL**, enter either the default domain or a custom domain for the Azure Active Directory, and append a unique string to it.</span></span> <span data-ttu-id="83224-125">在此範例中，使用了 **https://contoso5api.onmicrosoft.com** 的預設網域並指定尾碼 **/api**。</span><span class="sxs-lookup"><span data-stu-id="83224-125">In this example, the default domain of **https://contoso5api.onmicrosoft.com** is used with the suffix of **/api** specified.</span></span>

![新 Azure Active Directory 應用程式屬性][api-management-new-aad-application-2]

<span data-ttu-id="83224-127">按一下核取記號按鈕來儲存並建立應用程式，然後切換至 [設定] 索引標籤來設定新應用程式。</span><span class="sxs-lookup"><span data-stu-id="83224-127">Click the check button to save and create the application, and switch to the **Configure** tab to configure the new application.</span></span>

![新 Azure Active Directory 應用程式已建立][api-management-new-aad-app-created]

<span data-ttu-id="83224-129">如果將對這個應用程式使用多個 Azure Active Directory，請對 [應用程式是多租用戶] 按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="83224-129">If multiple Azure Active Directories are going to be used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="83224-130">預設值為 [ **否**]。</span><span class="sxs-lookup"><span data-stu-id="83224-130">The default is **No**.</span></span>

![是][api-management-aad-app-multi-tenant]

<span data-ttu-id="83224-132">從發佈者入口網站中 [外部身分識別] 索引標籤的 [Azure Active Directory] 區段，複製 [重新導向 URL]，並貼上至 [回覆 URL]。</span><span class="sxs-lookup"><span data-stu-id="83224-132">Copy the **Redirect URL** from the **Azure Active Directory** section of the **External Identities** tab in the publisher portal and paste it into the **Reply URL** text box.</span></span> 

![回覆 URL][api-management-aad-reply-url]

<span data-ttu-id="83224-134">捲動至設定索引標籤的底端，選取 [應用程式權限] 下拉式清單，並勾選 [讀取目錄資料]。</span><span class="sxs-lookup"><span data-stu-id="83224-134">Scroll to the bottom of the configure tab, select the **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![應用程式權限][api-management-aad-app-permissions]

<span data-ttu-id="83224-136">選取 [委派權限] 下拉式清單，並勾選 [啟用登入並讀取使用者的設定檔]。</span><span class="sxs-lookup"><span data-stu-id="83224-136">Select the **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![委派的權限][api-management-aad-delegated-permissions]

> <span data-ttu-id="83224-138">如需應用程式和委派的權限的詳細資訊，請參閱[存取 Graph API][Accessing the Graph API]。</span><span class="sxs-lookup"><span data-stu-id="83224-138">For more information about application and delegated permissions, see [Accessing the Graph API][Accessing the Graph API].</span></span>
> 
> 

<span data-ttu-id="83224-139">複製 [ **用戶端識別碼** ] 至剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="83224-139">Copy the **Client Id** to the clipboard.</span></span>

![用戶端識別碼][api-management-aad-app-client-id]

<span data-ttu-id="83224-141">切換回發行者入口網站，並將從 Azure Active Directory 應用程式組態複製的 [ **用戶端識別碼** ] 貼上。</span><span class="sxs-lookup"><span data-stu-id="83224-141">Switch back to the publisher portal and paste in the **Client Id** copied from the Azure Active Directory application configuration.</span></span>

![用戶端識別碼][api-management-client-id]

<span data-ttu-id="83224-143">切換回 Azure Active Directory 組態，並按一下 [金鑰] 區段中的 [選取持續時間] 下拉式清單，然後指定期間。</span><span class="sxs-lookup"><span data-stu-id="83224-143">Switch back to the Azure Active Directory configuration, and click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="83224-144">在此範例中使用 **1 年** 。</span><span class="sxs-lookup"><span data-stu-id="83224-144">In this example, **1 year** is used.</span></span>

![金鑰][api-management-aad-key-before-save]

<span data-ttu-id="83224-146">按一下 [ **儲存** ] 以儲存組態並顯示金鑰。</span><span class="sxs-lookup"><span data-stu-id="83224-146">Click **Save** to save the configuration and display the key.</span></span> <span data-ttu-id="83224-147">複製金鑰至剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="83224-147">Copy the key to the clipboard.</span></span>

> <span data-ttu-id="83224-148">記下此金鑰。</span><span class="sxs-lookup"><span data-stu-id="83224-148">Make a note of this key.</span></span> <span data-ttu-id="83224-149">關閉 Azure Active Directory 組態視窗之後，即無法再次顯示金鑰。</span><span class="sxs-lookup"><span data-stu-id="83224-149">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

![金鑰][api-management-aad-key-after-save]

<span data-ttu-id="83224-151">切換回發行者入口網站，並將金鑰貼上至 [ **用戶端密碼** ] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="83224-151">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

![用戶端密碼][api-management-client-secret]

<span data-ttu-id="83224-153">**允許的租用戶**  指定哪些目錄可存取 API 管理服務執行個體的 API。</span><span class="sxs-lookup"><span data-stu-id="83224-153">**Allowed Tenants** specifies which directories have access to the APIs of the API Management service instance.</span></span> <span data-ttu-id="83224-154">指定您要授與存取的 Azure Active Directory 執行個體的網域。</span><span class="sxs-lookup"><span data-stu-id="83224-154">Specify the domains of the Azure Active Directory instances to which you want to grant access.</span></span> <span data-ttu-id="83224-155">您可以使用換行符號、空格或逗號來分隔多個網域。</span><span class="sxs-lookup"><span data-stu-id="83224-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![允許的租用戶][api-management-client-allowed-tenants]


<span data-ttu-id="83224-157">指定需要的組態之後，按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="83224-157">Once the desired configuration is specified, click **Save**.</span></span>

![儲存][api-management-client-allowed-tenants-save]

<span data-ttu-id="83224-159">儲存變更之後，在指定 Azure Active Directory 中的使用者透過遵循[使用 Azure Active Directory 帳戶登入開發人員入口網站][Log in to the Developer portal using an Azure Active Directory account]中的步驟，即可登入開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="83224-159">Once the changes are saved, the users in the specified Azure Active Directory can sign in to the Developer portal by following the steps in [Log in to the Developer portal using an Azure Active Directory account][Log in to the Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="83224-160">可以在 [ **允許的租用戶** ] 區段中指定多個網域。</span><span class="sxs-lookup"><span data-stu-id="83224-160">Multiple domains can be specified in the **Allowed Tenants** section.</span></span> <span data-ttu-id="83224-161">在使用者可透過與註冊應用程式之原始網域不同的網域登入前，不同網域的全域管理員必須授與權限，應用程式才能存取目錄資料。</span><span class="sxs-lookup"><span data-stu-id="83224-161">Before any user can log in from a different domain than the original domain where the application was registered, a global administrator of the different domain must grant permission for the application to access directory data.</span></span> <span data-ttu-id="83224-162">若要授與權限，全域系統管理員應該移至 `https://<URL of your developer portal>/aadadminconsent` (例如，https://contoso.portal.azure-api.net/aadadminconsent)，輸入他們想要提供存取權之 Active Directory 租用戶的網域名稱，然後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="83224-162">To grant permission, the global administrator should go to `https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in the domain name of the Active Directory tenant they want to give access to and click Submit.</span></span> <span data-ttu-id="83224-163">在下列範例中，來自 `miaoaad.onmicrosoft.com` 的全域管理員嘗試給予這個特定開發人員入口網站的權限。</span><span class="sxs-lookup"><span data-stu-id="83224-163">In the following example, a global administrator from `miaoaad.onmicrosoft.com` is trying to give permission to this particular developer portal.</span></span> 

![權限][api-management-aad-consent]

<span data-ttu-id="83224-165">在下一個畫面中，系統會提示全域系統管理員確認要給予權限。</span><span class="sxs-lookup"><span data-stu-id="83224-165">In the next screen, the global administrator will be prompted to confirm giving the permission.</span></span> 

![權限][api-management-permissions-form]

> <span data-ttu-id="83224-167">如果非全域管理員在全域管理員授與其權限之前便嘗試登入，登入嘗試會失敗，並且顯示錯誤畫面。</span><span class="sxs-lookup"><span data-stu-id="83224-167">If a non-global administrator tries to log in before permissions are granted by a global administrator, the login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-to-add-an-external-azure-active-directory-group"></a><span data-ttu-id="83224-168">如何加入外部 Azure Active Directory 群組</span><span class="sxs-lookup"><span data-stu-id="83224-168">How to add an external Azure Active Directory Group</span></span>
<span data-ttu-id="83224-169">為 Azure Active Directory 中的使用者啟用存取之後，您可以將 Azure Active Directory 群組加入至 API 管理，以更輕鬆管理所需產品的群組中開發人員的關聯。</span><span class="sxs-lookup"><span data-stu-id="83224-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management to more easily manage the association of the developers in the group with the desired products.</span></span>

> <span data-ttu-id="83224-170">若要設定外部 Azure Active Directory 群組，必須先遵循上一節中的程序，在 [身分識別] 索引標籤中設定 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="83224-170">To configure an external Azure Active Directory group, the Azure Active Directory must first be configured in the Identities tab by following the procedure in the previous section.</span></span> 
> 
> 

<span data-ttu-id="83224-171">外部 Azure Active Directory 群組是從您要授與群組存取之產品的 [ **可見性** ] 索引標籤中加入。</span><span class="sxs-lookup"><span data-stu-id="83224-171">External Azure Active Directory groups are added from the **Visibility** tab of the product for which you wish to grant access to the group.</span></span> <span data-ttu-id="83224-172">按一下 [ **產品**]，然後按一下所需產品的名稱。</span><span class="sxs-lookup"><span data-stu-id="83224-172">Click **Products**, and then click the name of the desired product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="83224-174">切換至 [可見度] 索引標籤，然後按一下 [從 Azure Active Directory 新增群組]。</span><span class="sxs-lookup"><span data-stu-id="83224-174">Switch to the **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![加入群組][api-management-add-groups]

<span data-ttu-id="83224-176">從下拉式清單選取 [Azure Active Directory 租用戶]，然後在要新增的 [群組] 文字方塊中輸入所需群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="83224-176">Select the **Azure Active Directory Tenant** from the drop-down list, and then type the name of the desired group in the **Groups** to be added text box.</span></span>

![選取群組][api-management-select-group]

<span data-ttu-id="83224-178">此群組名稱可在您的 Azure Active Directory 的 [ **群組** ] 清單中找到，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="83224-178">This group name can be found in the **Groups** list for your Azure Active Directory, as shown in the following example.</span></span>

![Azure Active Directory 群組清單][api-management-aad-groups-list]

<span data-ttu-id="83224-180">按一下 [ **加入** ] 可驗證群組名稱並加入群組。</span><span class="sxs-lookup"><span data-stu-id="83224-180">Click **Add** to validate the group name and add the group.</span></span> <span data-ttu-id="83224-181">在此範例中會新增 **Contoso 5 Developers** 外部群組。</span><span class="sxs-lookup"><span data-stu-id="83224-181">In this example, the **Contoso 5 Developers** external group is added.</span></span> 

![Group added][api-management-aad-group-added]

<span data-ttu-id="83224-183">按一下 [ **儲存** ] 以儲存新群組選項。</span><span class="sxs-lookup"><span data-stu-id="83224-183">Click **Save** to save the new group selection.</span></span>

<span data-ttu-id="83224-184">透過一個產品設定 Azure Active Directory 群組之後，即可在 API 管理服務執行個體中其他產品的 [可見性] 索引標籤加以查看。</span><span class="sxs-lookup"><span data-stu-id="83224-184">Once an Azure Active Directory group has been configured from one product, it is available to be checked on the **Visibility** tab for the other products in the API Management service instance.</span></span>

<span data-ttu-id="83224-185">在加入外部群組之後，若要檢查並設定其屬性，請從 [群組] 索引標籤按一下群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="83224-185">To review and configure the properties for external groups once they have been added, click the name of the group from the **Groups** tab.</span></span>

![管理群組][api-management-groups]

<span data-ttu-id="83224-187">從此處，您可以編輯群組的 [名稱] 和 [說明]。</span><span class="sxs-lookup"><span data-stu-id="83224-187">From here you can edit the **Name** and the **Description** of the group.</span></span>

![編輯群組][api-management-edit-group]

<span data-ttu-id="83224-189">來自所設定 Azure Active Directory 的使用者可以登入開發人員入口網站，並透過下一節中的指示，以檢視及訂閱他們看的見的任何群組。</span><span class="sxs-lookup"><span data-stu-id="83224-189">Users from the configured Azure Active Directory can sign in to the Developer portal and view and subscribe to any groups for which they have visibility by following the instructions in the following section.</span></span>

## <a name="how-to-log-in-to-the-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="83224-190">如何使用 Azure Active Directory 帳戶登入開發人員入口網站</span><span class="sxs-lookup"><span data-stu-id="83224-190">How to log in to the Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="83224-191">若要使用前一節設定的 Azure Active Directory 帳戶登入開發人員入口網站，請使用來自 Active Directory 應用程式組態的 [登入 URL] 開啟新瀏覽器視窗，然後按一下 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="83224-191">To log into the Developer portal using an Azure Active Directory account configured in the previous sections, open a new browser window using the **Sign-on URL** from the Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![開發人員入口網站][api-management-dev-portal-signin]

<span data-ttu-id="83224-193">輸入您的 Azure Active Directory 中其中一個使用者的認證，然後按一下 [ **登入**]。</span><span class="sxs-lookup"><span data-stu-id="83224-193">Enter the credentials of one of the users in your Azure Active Directory, and click **Sign in**.</span></span>

![登入][api-management-aad-signin]

<span data-ttu-id="83224-195">如果需要其他資訊，可能會出現註冊表單的提示。</span><span class="sxs-lookup"><span data-stu-id="83224-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="83224-196">完成註冊表單，然後按一下 [ **註冊**]。</span><span class="sxs-lookup"><span data-stu-id="83224-196">Complete the registration form and click **Sign up**.</span></span>

![註冊][api-management-complete-registration]

<span data-ttu-id="83224-198">您的使用者現在已登入您的 API 服務執行個體的開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="83224-198">Your user is now logged into the developer portal for your API Management service instance.</span></span>

![註冊完成][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

