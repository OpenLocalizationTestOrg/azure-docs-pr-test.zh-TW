---
title: "應用程式服務的部署認證 aaaAzure |Microsoft 文件"
description: "了解如何 toouse hello Azure 應用程式服務的部署認證。"
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
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="5f674-103">設定 Azure App Service 的部署認證</span><span class="sxs-lookup"><span data-stu-id="5f674-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="5f674-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 支援兩種認證類，用於[本機 Git 部署](app-service-deploy-local-git.md)和 [FTP/S 部署](app-service-deploy-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="5f674-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="5f674-105">這些不是 hello 與 Azure Active Directory 認證相同。</span><span class="sxs-lookup"><span data-stu-id="5f674-105">These are not hello same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="5f674-106">**使用者層級認證**： 一組 hello 整個 Azure 帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="5f674-106">**User-level credentials**: one set of credentials for hello entire Azure account.</span></span> <span data-ttu-id="5f674-107">任何應用程式，任何訂用帳戶，hello Azure 帳戶中有權限 tooaccess，它可以是使用的 toodeploy tooApp 服務。</span><span class="sxs-lookup"><span data-stu-id="5f674-107">It can be used toodeploy tooApp Service for any app, in any subscription, that hello Azure account has permission tooaccess.</span></span> <span data-ttu-id="5f674-108">這些是您在設定的 hello 預設認證集**應用程式服務** > **&lt;app_name >** > **的部署認證**.</span><span class="sxs-lookup"><span data-stu-id="5f674-108">These are hello default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="5f674-109">這也是 hello 預設會顯示在 hello 入口網站 GUI (例如 hello**概觀**和**屬性**應用程式[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources))。</span><span class="sxs-lookup"><span data-stu-id="5f674-109">This is also hello default set that's surfaced in hello portal GUI (such as hello **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f674-110">當您委派存取 tooAzure 資源透過角色型存取控制 (RBAC) 或共同管理員權限時，每個接收存取 tooan 應用程式的 Azure 使用者可以使用自己的個人使用者層級認證，直到已撤銷存取權。</span><span class="sxs-lookup"><span data-stu-id="5f674-110">When you delegate access tooAzure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access tooan app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="5f674-111">這些部署認證不得與其他 Azure 使用者共用。</span><span class="sxs-lookup"><span data-stu-id="5f674-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="5f674-112">**應用程式層級認證**︰一組用於單個 應用程式的認證。</span><span class="sxs-lookup"><span data-stu-id="5f674-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="5f674-113">它可以是使用的 toodeploy toothat 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f674-113">It can be used toodeploy toothat app only.</span></span> <span data-ttu-id="5f674-114">hello 認證的每個應用程式於應用程式建立時自動產生，而且位於 hello 應用程式發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="5f674-114">hello credentials for each app is generated automatically at app creation, and is found in hello app's publish profile.</span></span> <span data-ttu-id="5f674-115">您無法手動設定 hello 認證，但是您可以加以重設應用程式的任何時間。</span><span class="sxs-lookup"><span data-stu-id="5f674-115">You cannot manually configure hello credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f674-116">在訂單 toogive 有人存取 toothese 認證透過角色型存取控制 (RBAC)，您需要 toomake 它們參與者或更高版本上 hello Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f674-116">In order toogive someone access toothese credentials via Role Based Access Control (RBAC), you need toomake them contributor or higher on hello Web App.</span></span> <span data-ttu-id="5f674-117">讀取器不允許 toopublish，，因此無法存取這些認證。</span><span class="sxs-lookup"><span data-stu-id="5f674-117">Readers are not allowed toopublish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="5f674-118"><a name="userscope"></a>設定及重設使用者層級的認證</span><span class="sxs-lookup"><span data-stu-id="5f674-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="5f674-119">您可以在任何應用程式的[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources)中，設定使用者層級認證。</span><span class="sxs-lookup"><span data-stu-id="5f674-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="5f674-120">無論哪個應用程式在您設定這些認證，它適用於 tooall 應用程式與 Azure 中的所有訂閱的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f674-120">Regardless in which app you configure these credentials, it applies tooall apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="5f674-121">tooconfigure 使用者層級認證：</span><span class="sxs-lookup"><span data-stu-id="5f674-121">tooconfigure your user-level credentials:</span></span>

1. <span data-ttu-id="5f674-122">在 hello [Azure 入口網站](https://portal.azure.com)，按一下 [應用程式服務] >  **&lt;any_app >** > **部署認證**。</span><span class="sxs-lookup"><span data-stu-id="5f674-122">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f674-123">在 hello 入口網站中，您必須擁有至少一個應用程式，才能存取 hello 部署認證 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5f674-123">In hello portal, you must have at least one app before you can access hello deployment credentials blade.</span></span> <span data-ttu-id="5f674-124">不過，與 hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)，您可以設定沒有現有的應用程式的使用者層級認證。</span><span class="sxs-lookup"><span data-stu-id="5f674-124">However, with hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="5f674-125">設定 hello 使用者名稱和密碼，然後再按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="5f674-125">Configure hello user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="5f674-126">一旦您已經設定您的部署認證，您可以找到 hello *Git*部署應用程式中的使用者名稱**概觀**，</span><span class="sxs-lookup"><span data-stu-id="5f674-126">Once you have set your deployment credentials, you can find hello *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="5f674-127">以及在應用程式的 [屬性] 中找到 「FTP」部署使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="5f674-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="5f674-128">Azure 不會顯示您的使用者層級部署密碼。</span><span class="sxs-lookup"><span data-stu-id="5f674-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="5f674-129">如果您忘記 hello 密碼時，您就無法再取回。</span><span class="sxs-lookup"><span data-stu-id="5f674-129">If you forget hello password, you can't retrieve it.</span></span> <span data-ttu-id="5f674-130">不過，您可以遵循本節中的 hello 步驟來重設您的認證。</span><span class="sxs-lookup"><span data-stu-id="5f674-130">However, you can reset your credentials by following hello steps in this section.</span></span>
>
>  

## <span data-ttu-id="5f674-131"><a name="appscope"></a>設定及重設應用程式層級的認證</span><span class="sxs-lookup"><span data-stu-id="5f674-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="5f674-132">App Service 中的每個應用程式，其應用程式層級的認證會儲存在 hello 中 XML 發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="5f674-132">For each app in App Service, its app-level credentials are stored in hello XML publish profile.</span></span>

<span data-ttu-id="5f674-133">tooget hello 應用程式層級的認證：</span><span class="sxs-lookup"><span data-stu-id="5f674-133">tooget hello app-level credentials:</span></span>

1. <span data-ttu-id="5f674-134">在 hello [Azure 入口網站](https://portal.azure.com)，按一下 [應用程式服務] >  **&lt;any_app >** > **概觀**。</span><span class="sxs-lookup"><span data-stu-id="5f674-134">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="5f674-135">按一下 [...更多]  >  [取得發行設定檔]，便會開始下載 .PublishSettings 檔案。</span><span class="sxs-lookup"><span data-stu-id="5f674-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="5f674-136">開啟 hello。PublishSettings 檔案，並尋找 hello `<publishProfile>` hello 屬性為`publishMethod="FTP"`。</span><span class="sxs-lookup"><span data-stu-id="5f674-136">Open hello .PublishSettings file and find hello `<publishProfile>` tag with hello attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="5f674-137">然後取得其 `userName` 和 `password` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5f674-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="5f674-138">這些是 hello 應用程式層級的認證。</span><span class="sxs-lookup"><span data-stu-id="5f674-138">These are hello app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="5f674-139">類似 toohello 使用者層級的認證，hello FTP 部署使用者名稱的格式的 hello `<app_name>\<username>`，只是 hello Git 部署使用者名稱和`<username>`hello 前面沒有`<app_name>\`。</span><span class="sxs-lookup"><span data-stu-id="5f674-139">Similar toohello user-level credentials, hello FTP deployment username is in hello format of `<app_name>\<username>`, and hello Git deployment username is just `<username>` without hello preceding `<app_name>\`.</span></span>

<span data-ttu-id="5f674-140">tooreset hello 應用程式層級的認證：</span><span class="sxs-lookup"><span data-stu-id="5f674-140">tooreset hello app-level credentials:</span></span>

1. <span data-ttu-id="5f674-141">在 hello [Azure 入口網站](https://portal.azure.com)，按一下 [應用程式服務] >  **&lt;any_app >** > **概觀**。</span><span class="sxs-lookup"><span data-stu-id="5f674-141">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="5f674-142">按一下 [...更多]  >  [重設發行設定檔]。</span><span class="sxs-lookup"><span data-stu-id="5f674-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="5f674-143">按一下**是**tooconfirm hello 重設。</span><span class="sxs-lookup"><span data-stu-id="5f674-143">Click **Yes** tooconfirm hello reset.</span></span>

    <span data-ttu-id="5f674-144">hello 重設動作會使任何先前下載。PublishSettings 檔案。</span><span class="sxs-lookup"><span data-stu-id="5f674-144">hello reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f674-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f674-145">Next steps</span></span>

<span data-ttu-id="5f674-146">了解如何 toouse 這些認證 toodeploy 應用程式從[本機 Git](app-service-deploy-local-git.md)或使用[FTP/S](app-service-deploy-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="5f674-146">Find out how toouse these credentials toodeploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
