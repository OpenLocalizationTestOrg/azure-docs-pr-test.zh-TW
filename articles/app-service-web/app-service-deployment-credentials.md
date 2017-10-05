---
title: "Azure App Service 部署認證 | Microsoft Docs"
description: "了解如何使用 Azure App Service 部署認證。"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 86a2cd8ae9f97c606a378452e44eec8941700531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="4ee22-103">設定 Azure App Service 的部署認證</span><span class="sxs-lookup"><span data-stu-id="4ee22-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="4ee22-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 支援兩種認證類，用於[本機 Git 部署](app-service-deploy-local-git.md)和 [FTP/S 部署](app-service-deploy-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="4ee22-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="4ee22-105">這些與您的 Azure Active Directory 認證不相同。</span><span class="sxs-lookup"><span data-stu-id="4ee22-105">These are not the same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="4ee22-106">**使用者層級認證**︰一組用於整個 Azure 帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="4ee22-106">**User-level credentials**: one set of credentials for the entire Azure account.</span></span> <span data-ttu-id="4ee22-107">它可以用來將任何應用程式部署至 Azure 帳戶有權存取的任何訂用帳戶的 App Service 中。</span><span class="sxs-lookup"><span data-stu-id="4ee22-107">It can be used to deploy to App Service for any app, in any subscription, that the Azure account has permission to access.</span></span> <span data-ttu-id="4ee22-108">有些預設認證集是在 [App Service]  >  [&lt;app_name>]  >  [部署認證] 中設定。</span><span class="sxs-lookup"><span data-stu-id="4ee22-108">These are the default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="4ee22-109">也有些預設認證集是呈現在入口網站 GUI 中 (例如應用程式的[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources)的 [概觀] 和 [屬性])。</span><span class="sxs-lookup"><span data-stu-id="4ee22-109">This is also the default set that's surfaced in the portal GUI (such as the **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4ee22-110">透過角色型存取控制 (RBAC) 或共同管理員權限委派 Azure 資源的存取權時，收到應用程式存取權的每個 Azure 使用者都可以使用他/她的個人使用者層級認證，直到存取權被撤銷為止。</span><span class="sxs-lookup"><span data-stu-id="4ee22-110">When you delegate access to Azure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access to an app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="4ee22-111">這些部署認證不得與其他 Azure 使用者共用。</span><span class="sxs-lookup"><span data-stu-id="4ee22-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="4ee22-112">**應用程式層級認證**︰一組用於單個 應用程式的認證。</span><span class="sxs-lookup"><span data-stu-id="4ee22-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="4ee22-113">它只可以用來部署該應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ee22-113">It can be used to deploy to that app only.</span></span> <span data-ttu-id="4ee22-114">每個應用程式的認證會在應用程式建立時自動產生，並且可以在應用程式的發行設定檔中找到。</span><span class="sxs-lookup"><span data-stu-id="4ee22-114">The credentials for each app is generated automatically at app creation, and is found in the app's publish profile.</span></span> <span data-ttu-id="4ee22-115">您無法以手動方式設定此認證，但您隨時可以為應用程式重設認證。</span><span class="sxs-lookup"><span data-stu-id="4ee22-115">You cannot manually configure the credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4ee22-116">若要透過角色型存取控制 (RBAC) 給予某人這些認證的存取權，您需要讓他們成為 Web 應用程式的參與者或更高級的角色。</span><span class="sxs-lookup"><span data-stu-id="4ee22-116">In order to give someone access to these credentials via Role Based Access Control (RBAC), you need to make them contributor or higher on the Web App.</span></span> <span data-ttu-id="4ee22-117">不允許發佈讀取器，因此無法存取這些認證。</span><span class="sxs-lookup"><span data-stu-id="4ee22-117">Readers are not allowed to publish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="4ee22-118"><a name="userscope"></a>設定及重設使用者層級的認證</span><span class="sxs-lookup"><span data-stu-id="4ee22-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="4ee22-119">您可以在任何應用程式的[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources)中，設定使用者層級認證。</span><span class="sxs-lookup"><span data-stu-id="4ee22-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="4ee22-120">無論在哪一個應用程式中設定這些認證，它都會套用至所有應用程式和您的 Azure 帳戶中的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ee22-120">Regardless in which app you configure these credentials, it applies to all apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="4ee22-121">設定使用者層級認證：</span><span class="sxs-lookup"><span data-stu-id="4ee22-121">To configure your user-level credentials:</span></span>

1. <span data-ttu-id="4ee22-122">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [App Service] > &lt;any_app>  >  [部署認證]。</span><span class="sxs-lookup"><span data-stu-id="4ee22-122">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4ee22-123">在入口網站中，您必須至少有一個應用程式，才能存取 [部署認證] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4ee22-123">In the portal, you must have at least one app before you can access the deployment credentials blade.</span></span> <span data-ttu-id="4ee22-124">不過，若使用 [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)，沒有現有應用程式也可以設定使用者層級認證。</span><span class="sxs-lookup"><span data-stu-id="4ee22-124">However, with the [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="4ee22-125">設定使用者名稱和密碼，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="4ee22-125">Configure the user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="4ee22-126">一旦設定好您的部署認證，就可以在應用程式的 [概觀] 中找到「Git」部署使用者名稱，</span><span class="sxs-lookup"><span data-stu-id="4ee22-126">Once you have set your deployment credentials, you can find the *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="4ee22-127">以及在應用程式的 [屬性] 中找到 「FTP」部署使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="4ee22-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="4ee22-128">Azure 不會顯示您的使用者層級部署密碼。</span><span class="sxs-lookup"><span data-stu-id="4ee22-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="4ee22-129">如果您忘記密碼，將無法取得密碼。</span><span class="sxs-lookup"><span data-stu-id="4ee22-129">If you forget the password, you can't retrieve it.</span></span> <span data-ttu-id="4ee22-130">不過，您可以依照本節的步驟來重設您的認證。</span><span class="sxs-lookup"><span data-stu-id="4ee22-130">However, you can reset your credentials by following the steps in this section.</span></span>
>
>  

## <span data-ttu-id="4ee22-131"><a name="appscope"></a>設定及重設應用程式層級的認證</span><span class="sxs-lookup"><span data-stu-id="4ee22-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="4ee22-132">App Service 中每個應用程式的認證會儲存在 XML 發佈設定檔中。</span><span class="sxs-lookup"><span data-stu-id="4ee22-132">For each app in App Service, its app-level credentials are stored in the XML publish profile.</span></span>

<span data-ttu-id="4ee22-133">若要取得應用程式層級的認證：</span><span class="sxs-lookup"><span data-stu-id="4ee22-133">To get the app-level credentials:</span></span>

1. <span data-ttu-id="4ee22-134">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [App Service] >[&lt;any_app>  >  [概觀]。</span><span class="sxs-lookup"><span data-stu-id="4ee22-134">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="4ee22-135">按一下 [...更多]  >  [取得發行設定檔]，便會開始下載 .PublishSettings 檔案。</span><span class="sxs-lookup"><span data-stu-id="4ee22-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="4ee22-136">開啟 .PublishSettings 檔案，找到包含 `publishMethod="FTP"` 屬性的 `<publishProfile>` 標籤。</span><span class="sxs-lookup"><span data-stu-id="4ee22-136">Open the .PublishSettings file and find the `<publishProfile>` tag with the attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="4ee22-137">然後取得其 `userName` 和 `password` 屬性。</span><span class="sxs-lookup"><span data-stu-id="4ee22-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="4ee22-138">這些就是應用程式層級的認證。</span><span class="sxs-lookup"><span data-stu-id="4ee22-138">These are the app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="4ee22-139">類似使用者層級認證，FTP 部署使用者名稱的格式是 `<app_name>\<username>`，Git 部署使用者名稱格式是 `<username>`，沒有前置的 `<app_name>\`。</span><span class="sxs-lookup"><span data-stu-id="4ee22-139">Similar to the user-level credentials, the FTP deployment username is in the format of `<app_name>\<username>`, and the Git deployment username is just `<username>` without the preceding `<app_name>\`.</span></span>

<span data-ttu-id="4ee22-140">若要重設應用程式層級的認證：</span><span class="sxs-lookup"><span data-stu-id="4ee22-140">To reset the app-level credentials:</span></span>

1. <span data-ttu-id="4ee22-141">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [App Service] >[&lt;any_app>  >  [概觀]。</span><span class="sxs-lookup"><span data-stu-id="4ee22-141">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="4ee22-142">按一下 [...更多]  >  [重設發行設定檔]。</span><span class="sxs-lookup"><span data-stu-id="4ee22-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="4ee22-143">按一下 [是] 確認重設。</span><span class="sxs-lookup"><span data-stu-id="4ee22-143">Click **Yes** to confirm the reset.</span></span>

    <span data-ttu-id="4ee22-144">重設動作會何先前下載的任何 .PublishSettings 檔案失效。</span><span class="sxs-lookup"><span data-stu-id="4ee22-144">The reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ee22-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ee22-145">Next steps</span></span>

<span data-ttu-id="4ee22-146">了解如何使用這些認證從[本機 Git](app-service-deploy-local-git.md)或使用[FTP/S](app-service-deploy-ftp.md) 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ee22-146">Find out how to use these credentials to deploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
