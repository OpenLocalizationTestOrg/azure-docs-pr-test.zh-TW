---
title: "aaaAdd 自訂網域和 SSL tooan Azure web 應用程式 |Microsoft 文件"
description: "了解如何 tooprepare Azure web 應用程式 toogo 生產藉由新增公司商標。 對應 hello 自訂網域名稱 （虛名網域） tooyour web 應用程式，並保護其安全的自訂 SSL 憑證。"
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
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a><span data-ttu-id="56159-104">新增自訂網域及 SSL tooan Azure web 應用程式</span><span class="sxs-lookup"><span data-stu-id="56159-104">Add custom domain and SSL tooan Azure web app</span></span>

<span data-ttu-id="56159-105">本教學課程會示範如何 tooquickly 對應自訂網域名稱 tooyour Azure web 應用程式，並使用 自訂的 SSL 憑證保護安全性。</span><span class="sxs-lookup"><span data-stu-id="56159-105">This tutorial shows you how tooquickly map a custom domain name tooyour Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="56159-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="56159-106">Before you begin</span></span>

<span data-ttu-id="56159-107">執行此範例之前，安裝 hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)在本機。</span><span class="sxs-lookup"><span data-stu-id="56159-107">Before running this sample, install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="56159-108">您也需要系統管理存取權 toohello DNS 設定 頁面，為個別網域提供者。</span><span class="sxs-lookup"><span data-stu-id="56159-108">You also need administrative access toohello DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="56159-109">例如，tooadd `www.contoso.com`，您需要 toobe 無法 tooconfigure DNS 項目`contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="56159-109">For example, tooadd `www.contoso.com`, you need toobe able tooconfigure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="56159-110">最後，您必須是有效的。PFX 檔案_和_其密碼，為您想 tooupload hello SSL 憑證並繫結。</span><span class="sxs-lookup"><span data-stu-id="56159-110">Lastly, you need a valid .PFX file _and_ its password for hello SSL certificate you want tooupload and bind.</span></span> <span data-ttu-id="56159-111">此 SSL 憑證應該是您想要設定的 toosecure hello 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="56159-111">This SSL certificate should be configured toosecure hello custom domain name you want.</span></span> <span data-ttu-id="56159-112">在上述範例中的 hello，保護您的 SSL 憑證應該`www.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="56159-112">In hello above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="56159-113">步驟 1 - 建立 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="56159-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="56159-114">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="56159-114">Log in tooAzure</span></span>

<span data-ttu-id="56159-115">我們正在進行 toouse hello Azure CLI 2.0 終端機視窗 toocreate hello 資源中的需要 toohost 我們在 Azure 中的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="56159-115">We are now going toouse hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost our Node.js app in Azure.</span></span>  <span data-ttu-id="56159-116">登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="56159-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="56159-117">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="56159-117">Create a resource group</span></span>   
<span data-ttu-id="56159-118">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="56159-118">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="56159-119">Azure 資源群組是在其中部署與管理 Azure 資源 (如 Web 應用程式、資料庫和儲存體帳戶) 的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="56159-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="56159-120">toosee 何種可能的值，您可以使用`---location`，使用 hello `az appservice list-locations` Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="56159-120">toosee what possible values you can use for `---location`, use hello `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="56159-121">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="56159-121">Create an App Service plan</span></span>

<span data-ttu-id="56159-122">建立應用程式服務方案以 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)命令。</span><span class="sxs-lookup"><span data-stu-id="56159-122">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="56159-123">hello 下列範例會建立名為 App Service 方案`myAppServicePlan`使用 hello**基本**定價層。</span><span class="sxs-lookup"><span data-stu-id="56159-123">hello following example creates an App Service plan named `myAppServicePlan` using hello **Basic** pricing tier.</span></span>

<span data-ttu-id="56159-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="56159-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="56159-125">Hello 應用程式服務方案建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例。</span><span class="sxs-lookup"><span data-stu-id="56159-125">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

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

## <a name="create-a-web-app"></a><span data-ttu-id="56159-126">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="56159-126">Create a web app</span></span>

<span data-ttu-id="56159-127">已建立 App Service 方案，建立 web 應用程式內 hello`myAppServicePlan`應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="56159-127">Now that an App Service plan has been created, create a web app within hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="56159-128">您正在裝載的空間 toodeploy 您的程式碼，以及為您提供 URL tooview hello hello web 應用程式提供部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="56159-128">hello web app gives your a hosting space toodeploy your code as well as provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="56159-129">使用 hello [az 應用程式 web 建立](/cli/azure/appservice/web#create)命令 toocreate hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="56159-129">Use hello [az appservice web create](/cli/azure/appservice/web#create) command toocreate hello web app.</span></span> 

<span data-ttu-id="56159-130">在下方的 hello 命令，請取代您自己的唯一應用程式名稱，您會看到 hello`<app_name>`預留位置。</span><span class="sxs-lookup"><span data-stu-id="56159-130">In hello command below, please substitute your own unique app name where you see hello `<app_name>` placeholder.</span></span> <span data-ttu-id="56159-131">這個唯一名稱會用做為 hello hello hello web 應用程式的預設網域名稱的一部分，因此 hello 名稱需要 toobe 唯一跨 Azure 中的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="56159-131">This unique name will be used as hello part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="56159-132">公開 tooyour 使用者之前，您稍後可以對應任何自訂 DNS 項目 toohello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="56159-132">You can later map any custom DNS entry toohello web app before you expose it tooyour users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="56159-133">Hello web 應用程式建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例。</span><span class="sxs-lookup"><span data-stu-id="56159-133">When hello web app has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

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

<span data-ttu-id="56159-134">從 JSON 輸出 hello`defaultHostName`顯示 web 應用程式的預設網域名稱。</span><span class="sxs-lookup"><span data-stu-id="56159-134">From hello JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="56159-135">在瀏覽器中瀏覽 toothis 位址。</span><span class="sxs-lookup"><span data-stu-id="56159-135">In your browser, navigate toothis address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="56159-137">步驟 2 - 設定 DNS 對應</span><span class="sxs-lookup"><span data-stu-id="56159-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="56159-138">在此步驟中，您必須加入的對應自訂網域 tooyour web 應用程式的預設網域名稱，從`<app_name>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="56159-138">In this step, you add a mapping from a custom domain tooyour web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="56159-139">一般而言，您可以在網域提供者的網站中執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="56159-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="56159-140">每個網域註冊機構的網站稍有不同，請查閱您的提供者文件。</span><span class="sxs-lookup"><span data-stu-id="56159-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="56159-141">不過，以下有幾個一般方針。</span><span class="sxs-lookup"><span data-stu-id="56159-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-tootoodns-management-page"></a><span data-ttu-id="56159-142">瀏覽 tootooDNS 管理頁面</span><span class="sxs-lookup"><span data-stu-id="56159-142">Navigate tootooDNS management page</span></span>

<span data-ttu-id="56159-143">首先，登入 tooyour 網域註冊機構的網站。</span><span class="sxs-lookup"><span data-stu-id="56159-143">First, log in tooyour domain registrar's website.</span></span>  

<span data-ttu-id="56159-144">然後，尋找 hello 頁面管理 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="56159-144">Then, find hello page for managing DNS records.</span></span> <span data-ttu-id="56159-145">尋找連結或標示為 hello 網站的區域**網域名稱**， **DNS**，或**名稱伺服器管理**。</span><span class="sxs-lookup"><span data-stu-id="56159-145">Look for links or areas of hello site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="56159-146">通常，您可以找到 hello 連結，檢視您的帳戶資訊，例如尋找連結**我的網域**。</span><span class="sxs-lookup"><span data-stu-id="56159-146">Often, you can find hello link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="56159-147">找到此頁面之後，尋找可讓您新增或編輯 DNS 記錄的連結。</span><span class="sxs-lookup"><span data-stu-id="56159-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="56159-148">這可能是 [區域檔案]、[DNS 記錄] 連結，或 [進階設定] 連結。</span><span class="sxs-lookup"><span data-stu-id="56159-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="56159-149">建立 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="56159-149">Create a CNAME record</span></span>

<span data-ttu-id="56159-150">新增對應 hello 所需的子網域名稱 tooyour web 應用程式的預設網域名稱的 CNAME 記錄 (`<app_name>.azurewebsites.net`，其中`<app_name>`是您的應用程式的唯一名稱)。</span><span class="sxs-lookup"><span data-stu-id="56159-150">Add a CNAME record that maps hello desired subdomain name tooyour web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="56159-151">Hello`www.contoso.com`範例中，建立 CNAME 對應 hello `www` hostname 太`<app_name>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="56159-151">For hello `www.contoso.com` example, you create a CNAME that maps hello `www` hostname too`<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a><span data-ttu-id="56159-152">步驟 3-設定 web 應用程式上的 hello 自訂網域</span><span class="sxs-lookup"><span data-stu-id="56159-152">Step 3 - Configure hello custom domain on your web app</span></span>

<span data-ttu-id="56159-153">當您完成設定 hello 主機名稱的對應網域提供者的網站中時，您已準備好 tooconfigure hello 自訂網域 web 應用程式上。</span><span class="sxs-lookup"><span data-stu-id="56159-153">When you finish configuring hello hostname mapping in your domain provider's website, you're ready tooconfigure hello custom domain on your web app.</span></span> <span data-ttu-id="56159-154">使用 hello [az appservice web 設定主機名稱加入](/cli/azure/appservice/web/config/hostname#add)命令 tooadd 這項設定。</span><span class="sxs-lookup"><span data-stu-id="56159-154">Use hello [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command tooadd this configuration.</span></span> 

<span data-ttu-id="56159-155">在下方的 hello 命令，請取代`<app_name>`與您的唯一應用程式名稱 < your_custom_domain > hello 完整格式的自訂網域名稱 (例如`www.contoso.com`)。</span><span class="sxs-lookup"><span data-stu-id="56159-155">In hello command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with hello fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="56159-156">hello 自訂網域，現在是完全對應的 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="56159-156">hello custom domain now is fully mapped tooyour web app.</span></span> <span data-ttu-id="56159-157">在瀏覽器中瀏覽 toohello 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="56159-157">In your browser, navigate toohello custom domain name.</span></span> <span data-ttu-id="56159-158">例如：</span><span class="sxs-lookup"><span data-stu-id="56159-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a><span data-ttu-id="56159-160">步驟 4-繫結的自訂 SSL 憑證 tooyour web 應用程式</span><span class="sxs-lookup"><span data-stu-id="56159-160">Step 4 - Bind a custom SSL certificate tooyour web app</span></span>

<span data-ttu-id="56159-161">現在您已經有 Azure web 應用程式，您想要 hello 瀏覽器的網址列中的 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="56159-161">You now have an Azure web app, with hello domain name you want in hello browser's address bar.</span></span> <span data-ttu-id="56159-162">不過，如果您瀏覽 toohello`https://<your_custom_domain>`現在，您會收到憑證錯誤。</span><span class="sxs-lookup"><span data-stu-id="56159-162">However, if you navigate toohello `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="56159-164">發生此錯誤是因為 Web 應用程式尚無符合自訂網域名稱的 SSL 憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="56159-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="56159-165">不過，您無法取得錯誤如果您瀏覽過`https://<app_name>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="56159-165">However, you don't get an error if you navigate too`https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="56159-166">這是因為您的應用程式，以及所有的 Azure App Service 應用程式，使用 hello SSL 憑證保護 hello`*.azurewebsites.net`預設萬用字元網域。</span><span class="sxs-lookup"><span data-stu-id="56159-166">This is because your app, as well as all Azure App Service apps, is secured with hello SSL certificate for hello `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="56159-167">在您的自訂網域名稱來排序 tooaccess 您 web 應用程式，您需要 toobind hello SSL 憑證 toohello web 應用程式的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="56159-167">In order tooaccess your web app by your custom domain name, you need toobind hello SSL certificate for your custom domain toohello web app.</span></span> <span data-ttu-id="56159-168">您將在此步驟中這樣做。</span><span class="sxs-lookup"><span data-stu-id="56159-168">You will do it in this step.</span></span> 

### <a name="upload-hello-ssl-certificate"></a><span data-ttu-id="56159-169">上傳 hello SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="56159-169">Upload hello SSL certificate</span></span>

<span data-ttu-id="56159-170">Hello tooyour web 應用程式的自訂網域的 SSL 憑證上傳使用 hello [az appservice web 設定 ssl 上傳](/cli/azure/appservice/web/config/ssl#upload)命令。</span><span class="sxs-lookup"><span data-stu-id="56159-170">Upload hello SSL certificate for your custom domain tooyour web app by using hello [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="56159-171">在下方的 hello 命令，請取代`<app_name>`具有唯一的應用程式名稱`<path_to_ptx_file>`與 hello 路徑 tooyour。PFX 檔案和`<password>`與憑證的密碼。</span><span class="sxs-lookup"><span data-stu-id="56159-171">In hello command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with hello path tooyour .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="56159-172">上傳 hello 憑證時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="56159-172">When hello certificate is uploaded, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="56159-173">從 JSON 輸出 hello`thumbprint`顯示您上傳的憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="56159-173">From hello JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="56159-174">將複製的值供 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="56159-174">Copy its value for hello next step.</span></span>

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a><span data-ttu-id="56159-175">繫結 hello 上傳 SSL 憑證 toohello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="56159-175">Bind hello uploaded SSL certificate toohello web app</span></span>

<span data-ttu-id="56159-176">您的 web 應用程式現在具有您想，hello 自訂網域名稱，而且也有保護該自訂網域的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="56159-176">Your web app now has hello custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="56159-177">hello 事左的 toodo 是 toobind hello 上傳的憑證 toohello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="56159-177">hello only thing left toodo is toobind hello uploaded certificate toohello web app.</span></span> <span data-ttu-id="56159-178">您可以使用 hello [az appservice web 設定 ssl 繫結](/cli/azure/appservice/web/config/ssl#bind)命令。</span><span class="sxs-lookup"><span data-stu-id="56159-178">You do this by using hello [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="56159-179">在下方的 hello 命令，請取代`<app_name>`具有唯一的應用程式名稱和`<thumbprint-from-previous-output>`hello 您從 hello 前一個命令取得的憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="56159-179">In hello command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with hello certificate thumbprint that you get from hello previous command.</span></span> 

<span data-ttu-id="56159-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="56159-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="56159-181">Hello 憑證繫結的 tooyour web 應用程式時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="56159-181">When hello certificate is bound tooyour web app, hello Azure CLI shows information similar toohello following example:</span></span>

<span data-ttu-id="56159-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="56159-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="56159-183">在瀏覽器中瀏覽 tooHTTPS 端點的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="56159-183">In your browser, navigate tooHTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="56159-184">例如：</span><span class="sxs-lookup"><span data-stu-id="56159-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="56159-186">其他資源</span><span class="sxs-lookup"><span data-stu-id="56159-186">More resources</span></span>

<span data-ttu-id="56159-187">[購買自訂網域名稱並在 Azure App Service 中設定](custom-dns-web-site-buydomains-web-app.md)
[購買並設定 Azure App Service 的 SSL 憑證](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="56159-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
