---
title: "將自訂網域和 SSL 新增至 Azure Web 應用程式 | Microsoft Docs"
description: "了解如何新增公司商標以準備將 Azure Web 應用程式移至生產環境。 將自訂網域名稱 (虛名網域) 對應至 Web 應用程式，並使用自訂 SSL 憑證保護它。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c9d00f678b6257a8aafb35acd2d5a2292703a2dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="add-custom-domain-and-ssl-to-an-azure-web-app"></a><span data-ttu-id="178ff-104">將自訂網域和 SSL 新增至 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="178ff-104">Add custom domain and SSL to an Azure web app</span></span>

<span data-ttu-id="178ff-105">本教學課程示範如何快速地將自訂網域名稱對應至 Azure Web 應用程式，然後使用自訂 SSL 憑證保護它。</span><span class="sxs-lookup"><span data-stu-id="178ff-105">This tutorial shows you how to quickly map a custom domain name to your Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="178ff-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="178ff-106">Before you begin</span></span>

<span data-ttu-id="178ff-107">執行此範例之前，請在本機安裝 [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="178ff-107">Before running this sample, install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="178ff-108">對於您各自網域提供者的 DNS 設定頁面，您也需要有系統管理存取權。</span><span class="sxs-lookup"><span data-stu-id="178ff-108">You also need administrative access to the DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="178ff-109">例如，若要新增 `www.contoso.com`，您必須能夠設定 `contoso.com` 的 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="178ff-109">For example, to add `www.contoso.com`, you need to be able to configure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="178ff-110">稍後，對於您想要上傳和繫結的 SSL 憑證，您需要具備有效的 .PFX 檔案_和_其密碼。</span><span class="sxs-lookup"><span data-stu-id="178ff-110">Lastly, you need a valid .PFX file _and_ its password for the SSL certificate you want to upload and bind.</span></span> <span data-ttu-id="178ff-111">此 SSL 憑證應該設定為保護您想要的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="178ff-111">This SSL certificate should be configured to secure the custom domain name you want.</span></span> <span data-ttu-id="178ff-112">在上述範例中，您的 SSL 憑證應該保護 `www.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="178ff-112">In the above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="178ff-113">步驟 1 - 建立 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="178ff-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="178ff-114">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="178ff-114">Log in to Azure</span></span>

<span data-ttu-id="178ff-115">我們現在會在終端機視窗中使用 Azure CLI 2.0 ，以建立在 Azure 中裝載 Node.js 應用程式所需的資源。</span><span class="sxs-lookup"><span data-stu-id="178ff-115">We are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host our Node.js app in Azure.</span></span>  <span data-ttu-id="178ff-116">使用 [az login](/cli/azure/#login) 命令登入 Azure 訂用帳戶並遵循畫面上的指示。</span><span class="sxs-lookup"><span data-stu-id="178ff-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="178ff-117">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="178ff-117">Create a resource group</span></span>   
<span data-ttu-id="178ff-118">使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="178ff-118">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="178ff-119">Azure 資源群組是在其中部署與管理 Azure 資源 (如 Web 應用程式、資料庫和儲存體帳戶) 的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="178ff-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="178ff-120">若要查看您可用於 `---location` 的可能值，請使用 `az appservice list-locations` Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="178ff-120">To see what possible values you can use for `---location`, use the `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="178ff-121">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="178ff-121">Create an App Service plan</span></span>

<span data-ttu-id="178ff-122">使用 [az appservice plan create](/cli/azure/appservice/plan#create) 命令來建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="178ff-122">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="178ff-123">下列範例使用**基本**定價層，建立名為 `myAppServicePlan` 的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="178ff-123">The following example creates an App Service plan named `myAppServicePlan` using the **Basic** pricing tier.</span></span>

<span data-ttu-id="178ff-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="178ff-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="178ff-125">建立 App Service 方案後，Azure CLI 會顯示類似下列範例的資訊。</span><span class="sxs-lookup"><span data-stu-id="178ff-125">When the App Service plan has been created, the Azure CLI shows information similar to the following example.</span></span> 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a><span data-ttu-id="178ff-126">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="178ff-126">Create a web app</span></span>

<span data-ttu-id="178ff-127">現已建立 App Service 方案，請在 `myAppServicePlan` App Service 方案中建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="178ff-127">Now that an App Service plan has been created, create a web app within the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="178ff-128">此 Web 應用程式會為您提供裝載空間來部署程式碼，也會提供 URL 讓您檢視已部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="178ff-128">The web app gives your a hosting space to deploy your code as well as provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="178ff-129">使用 [az appservice web create](/cli/azure/appservice/web#create) 命令建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="178ff-129">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the web app.</span></span> 

<span data-ttu-id="178ff-130">在下列命令中，請將 `<app_name>` 預留位置替換成您自己的唯一應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="178ff-130">In the command below, please substitute your own unique app name where you see the `<app_name>` placeholder.</span></span> <span data-ttu-id="178ff-131">這個唯一名稱將用來作為 Web 應用程式預設網域名稱的一部分，因此，這個名稱在 Azure 的所有應用程式中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="178ff-131">This unique name will be used as the part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="178ff-132">您稍後先將任何自訂 DNS 項目對應至 Web 應用程式，再將它公開給使用者。</span><span class="sxs-lookup"><span data-stu-id="178ff-132">You can later map any custom DNS entry to the web app before you expose it to your users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="178ff-133">建立 Web 應用程式後，Azure CLI 會顯示類似下列範例的資訊。</span><span class="sxs-lookup"><span data-stu-id="178ff-133">When the web app has been created, the Azure CLI shows information similar to the following example.</span></span> 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

<span data-ttu-id="178ff-134">從 JSON 輸出中，`defaultHostName` 會顯示 Web 應用程式的預設網域名稱。</span><span class="sxs-lookup"><span data-stu-id="178ff-134">From the JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="178ff-135">在瀏覽器中，瀏覽至此位址。</span><span class="sxs-lookup"><span data-stu-id="178ff-135">In your browser, navigate to this address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="178ff-137">步驟 2 - 設定 DNS 對應</span><span class="sxs-lookup"><span data-stu-id="178ff-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="178ff-138">在此步驟中，您將新增從自訂網域至 Web 應用程式預設網域名稱 (`<app_name>.azurewebsites.net`) 的對應。</span><span class="sxs-lookup"><span data-stu-id="178ff-138">In this step, you add a mapping from a custom domain to your web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="178ff-139">一般而言，您可以在網域提供者的網站中執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="178ff-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="178ff-140">每個網域註冊機構的網站稍有不同，請查閱您的提供者文件。</span><span class="sxs-lookup"><span data-stu-id="178ff-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="178ff-141">不過，以下有幾個一般方針。</span><span class="sxs-lookup"><span data-stu-id="178ff-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-to-to-dns-management-page"></a><span data-ttu-id="178ff-142">瀏覽至 DNS 管理頁面</span><span class="sxs-lookup"><span data-stu-id="178ff-142">Navigate to to DNS management page</span></span>

<span data-ttu-id="178ff-143">首先，登入網域註冊機構的網站。</span><span class="sxs-lookup"><span data-stu-id="178ff-143">First, log in to your domain registrar's website.</span></span>  

<span data-ttu-id="178ff-144">然後，尋找 DNS 記錄的管理頁面。</span><span class="sxs-lookup"><span data-stu-id="178ff-144">Then, find the page for managing DNS records.</span></span> <span data-ttu-id="178ff-145">在網站中尋找標示為**網域名稱**、**DNS** 或**名稱伺服器管理**的連結或區域。</span><span class="sxs-lookup"><span data-stu-id="178ff-145">Look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="178ff-146">通常可透過檢視您的帳戶資訊，然後尋找 **我的網域**之類的連結來找到此連結。</span><span class="sxs-lookup"><span data-stu-id="178ff-146">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="178ff-147">找到此頁面之後，尋找可讓您新增或編輯 DNS 記錄的連結。</span><span class="sxs-lookup"><span data-stu-id="178ff-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="178ff-148">這可能是 [區域檔案]、[DNS 記錄] 連結，或 [進階設定] 連結。</span><span class="sxs-lookup"><span data-stu-id="178ff-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="178ff-149">建立 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="178ff-149">Create a CNAME record</span></span>

<span data-ttu-id="178ff-150">新增 CNAME 記錄，將所需的子網域名稱對應至 Web 應用程式的預設網域名稱 (`<app_name>.azurewebsites.net`，其中 `<app_name>` 是應用程式的唯一名稱)。</span><span class="sxs-lookup"><span data-stu-id="178ff-150">Add a CNAME record that maps the desired subdomain name to your web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="178ff-151">在 `www.contoso.com` 範例中，建立 CNAME 將 `www` 主機名稱對應至 `<app_name>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="178ff-151">For the `www.contoso.com` example, you create a CNAME that maps the `www` hostname to `<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-the-custom-domain-on-your-web-app"></a><span data-ttu-id="178ff-152">步驟 3 - 在 Web 應用程式上設定自訂網域</span><span class="sxs-lookup"><span data-stu-id="178ff-152">Step 3 - Configure the custom domain on your web app</span></span>

<span data-ttu-id="178ff-153">當您在網域提供者的網站中完成設定主機名稱對應時，就可以準備在 Web 應用程式上設定自訂網域。</span><span class="sxs-lookup"><span data-stu-id="178ff-153">When you finish configuring the hostname mapping in your domain provider's website, you're ready to configure the custom domain on your web app.</span></span> <span data-ttu-id="178ff-154">使用 [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) 命令新增這項設定。</span><span class="sxs-lookup"><span data-stu-id="178ff-154">Use the [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command to add this configuration.</span></span> 

<span data-ttu-id="178ff-155">在下列命令，請將 `<app_name>` 替換成唯一的應用程式名稱，將 <your_custom_domain> 替換成完整的自訂網域名稱 (例如 `www.contoso.com`)。</span><span class="sxs-lookup"><span data-stu-id="178ff-155">In the command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with the fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="178ff-156">自訂網域現在已完全對應至您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="178ff-156">The custom domain now is fully mapped to your web app.</span></span> <span data-ttu-id="178ff-157">在瀏覽器中，瀏覽至自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="178ff-157">In your browser, navigate to the custom domain name.</span></span> <span data-ttu-id="178ff-158">例如：</span><span class="sxs-lookup"><span data-stu-id="178ff-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-to-your-web-app"></a><span data-ttu-id="178ff-160">步驟 4 - 將自訂 SSL 憑證繫結至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="178ff-160">Step 4 - Bind a custom SSL certificate to your web app</span></span>

<span data-ttu-id="178ff-161">您現在有 Azure Web 應用程式，在瀏覽器的網址列中也有您要的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="178ff-161">You now have an Azure web app, with the domain name you want in the browser's address bar.</span></span> <span data-ttu-id="178ff-162">但是，如果您現在就瀏覽至 `https://<your_custom_domain>`，則會發生憑證錯誤。</span><span class="sxs-lookup"><span data-stu-id="178ff-162">However, if you navigate to the `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="178ff-164">發生此錯誤是因為 Web 應用程式尚無符合自訂網域名稱的 SSL 憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="178ff-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="178ff-165">不過，如果瀏覽至 `https://<app_name>.azurewebsites.net`，則不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="178ff-165">However, you don't get an error if you navigate to `https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="178ff-166">這是因為預設會使用 `*.azurewebsites.net` 萬用字元網域的 SSL 憑證，保護您的應用程式和所有 Azure App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="178ff-166">This is because your app, as well as all Azure App Service apps, is secured with the SSL certificate for the `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="178ff-167">若要以自訂網域名稱存取 Web 應用程式的，您需要將自訂網域的 SSL 憑證繫結至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="178ff-167">In order to access your web app by your custom domain name, you need to bind the SSL certificate for your custom domain to the web app.</span></span> <span data-ttu-id="178ff-168">您將在此步驟中這樣做。</span><span class="sxs-lookup"><span data-stu-id="178ff-168">You will do it in this step.</span></span> 

### <a name="upload-the-ssl-certificate"></a><span data-ttu-id="178ff-169">上傳 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="178ff-169">Upload the SSL certificate</span></span>

<span data-ttu-id="178ff-170">使用 [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) 命令，將自訂網域的 SSL 憑證上傳至您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="178ff-170">Upload the SSL certificate for your custom domain to your web app by using the [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="178ff-171">在下列命令中，請將 `<app_name>` 替換成唯一的應用程式名稱，將 `<path_to_ptx_file>` 替換成 .PFX 檔案的路徑，將 `<password>` 替換成憑證的密碼。</span><span class="sxs-lookup"><span data-stu-id="178ff-171">In the command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with the path to your .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="178ff-172">上傳憑證之後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="178ff-172">When the certificate is uploaded, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

<span data-ttu-id="178ff-173">從 JSON 輸出中，`thumbprint` 會顯示您已上傳之憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="178ff-173">From the JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="178ff-174">複製它的值供下一個步驟使用。</span><span class="sxs-lookup"><span data-stu-id="178ff-174">Copy its value for the next step.</span></span>

### <a name="bind-the-uploaded-ssl-certificate-to-the-web-app"></a><span data-ttu-id="178ff-175">將上傳的 SSL 憑證繫結至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="178ff-175">Bind the uploaded SSL certificate to the web app</span></span>

<span data-ttu-id="178ff-176">Web 應用程式現在有您想要的自訂網域名稱，也有可保護該自訂網域的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="178ff-176">Your web app now has the custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="178ff-177">剩下的工作就是將已上傳的憑證繫結至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="178ff-177">The only thing left to do is to bind the uploaded certificate to the web app.</span></span> <span data-ttu-id="178ff-178">您可以使用 [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) 命令這樣做。</span><span class="sxs-lookup"><span data-stu-id="178ff-178">You do this by using the [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="178ff-179">在下列命令中，請將 `<app_name>` 替換成唯一的應用程式名稱，將 `<thumbprint-from-previous-output>` 替換成您從上一個命令取得的憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="178ff-179">In the command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with the certificate thumbprint that you get from the previous command.</span></span> 

<span data-ttu-id="178ff-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="178ff-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="178ff-181">憑證繫結至 Web 應用程式之後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="178ff-181">When the certificate is bound to your web app, the Azure CLI shows information similar to the following example:</span></span>

<span data-ttu-id="178ff-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="178ff-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="178ff-183">在瀏覽器中，瀏覽至自訂網域名稱的 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="178ff-183">In your browser, navigate to HTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="178ff-184">例如：</span><span class="sxs-lookup"><span data-stu-id="178ff-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="178ff-186">其他資源</span><span class="sxs-lookup"><span data-stu-id="178ff-186">More resources</span></span>

<span data-ttu-id="178ff-187">[購買自訂網域名稱並在 Azure App Service 中設定](custom-dns-web-site-buydomains-web-app.md)
[購買並設定 Azure App Service 的 SSL 憑證](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="178ff-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
