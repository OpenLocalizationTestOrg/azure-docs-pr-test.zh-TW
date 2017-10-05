---
title: "使用 Azure CLI 建立 Azure App 的身分識別 | Microsoft Docs"
description: "描述如何使用 Azure CLI 建立 Azure Active Directory 應用程式和服務主體，並透過角色型存取控制將存取權授與資源。 它示範如何使用密碼或憑證來驗證應用程式。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 3c5826d58887ff1af4df8e66999d9c1a1643bcc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-cli-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="98864-104">使用 Azure CLI 建立用來存取資源的服務主體</span><span class="sxs-lookup"><span data-stu-id="98864-104">Use Azure CLI to create a service principal to access resources</span></span>

<span data-ttu-id="98864-105">當您有 App 或指令碼需要存取資源時，可以設定 App 的身分識別，並使用 App 自己的認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="98864-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="98864-106">此身分識別就是所謂的服務主體。</span><span class="sxs-lookup"><span data-stu-id="98864-106">This identity is known as a service principal.</span></span> <span data-ttu-id="98864-107">這種方法可讓您︰</span><span class="sxs-lookup"><span data-stu-id="98864-107">This approach enables you to:</span></span>

* <span data-ttu-id="98864-108">將權限指派給不同於您自己權限的 App 身分識別。</span><span class="sxs-lookup"><span data-stu-id="98864-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="98864-109">一般而言，這些權限只會限制為 App 必須執行的確切權限。</span><span class="sxs-lookup"><span data-stu-id="98864-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="98864-110">使用憑證在執行無人看管的指令碼時進行驗證。</span><span class="sxs-lookup"><span data-stu-id="98864-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="98864-111">本文說明如何使用 [Azure CLI 1.0](../cli-install-nodejs.md) 來設定應用程式，讓它利用自己的認證和身分識別來執行。</span><span class="sxs-lookup"><span data-stu-id="98864-111">This article shows you how to use [Azure CLI 1.0](../cli-install-nodejs.md) to set up an application to run under its own credentials and identity.</span></span> <span data-ttu-id="98864-112">安裝最新版的 [Azure CLI 1.0](../cli-install-nodejs.md)，以確定您的環境符合本文中的範例。</span><span class="sxs-lookup"><span data-stu-id="98864-112">Install the latest version of [Azure CLI 1.0](../cli-install-nodejs.md) to make sure your environment matches the examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="98864-113">所需的權限</span><span class="sxs-lookup"><span data-stu-id="98864-113">Required permissions</span></span>
<span data-ttu-id="98864-114">若要完成本主題，您必須在 Azure Active Directory 和您的 Azure 訂用帳戶中有足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="98864-114">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="98864-115">具體來說，您必須能夠在 Azure Active Directory 中建立應用程式，並將服務主體指派給角色。</span><span class="sxs-lookup"><span data-stu-id="98864-115">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="98864-116">檢查您的帳戶是否具有足夠的權限，最簡單的方式是透過入口網站。</span><span class="sxs-lookup"><span data-stu-id="98864-116">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="98864-117">請參閱[在入口網站中檢查必要的權限](resource-group-create-service-principal-portal.md#required-permissions)。</span><span class="sxs-lookup"><span data-stu-id="98864-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="98864-118">現在，繼續進行[密碼](#create-service-principal-with-password)或[憑證](#create-service-principal-with-certificate)驗證的章節。</span><span class="sxs-lookup"><span data-stu-id="98864-118">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="98864-119">使用密碼建立服務主體</span><span class="sxs-lookup"><span data-stu-id="98864-119">Create service principal with password</span></span>
<span data-ttu-id="98864-120">在本節中，您可以執行步驟來使用密碼建立 AD 應用程式，並將讀取者角色指派給服務主體。</span><span class="sxs-lookup"><span data-stu-id="98864-120">In this section, you perform the steps to create the AD application with a password, and assign the Reader role to the service principal.</span></span>

1. <span data-ttu-id="98864-121">登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="98864-121">Sign in to your account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="98864-122">若要建立應用程式身分識別，請提供 App 名稱和密碼，如下列命令中所示︰</span><span class="sxs-lookup"><span data-stu-id="98864-122">To create an app identity, provide the name of the app and a password, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="98864-123">傳回新的服務主體。</span><span class="sxs-lookup"><span data-stu-id="98864-123">The new service principal is returned.</span></span> <span data-ttu-id="98864-124">授與權限時，需要物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="98864-124">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="98864-125">在登入時，則需要隨服務主體名稱列出的 GUID。</span><span class="sxs-lookup"><span data-stu-id="98864-125">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="98864-126">此 GUID 是和應用程式識別碼相同的值。</span><span class="sxs-lookup"><span data-stu-id="98864-126">This guid is the same value as the app id.</span></span> <span data-ttu-id="98864-127">在範例應用程式中，這個值稱為 `Client ID`。</span><span class="sxs-lookup"><span data-stu-id="98864-127">In the sample applications, this value is referred to as the `Client ID`.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. <span data-ttu-id="98864-128">授與服務主體對您訂用帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="98864-128">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="98864-129">在此範例中，您會將服務主體新增至「讀取者」角色，以授與讀取訂用帳戶中所有資源的權限。</span><span class="sxs-lookup"><span data-stu-id="98864-129">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="98864-130">若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="98864-130">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="98864-131">針對 objectid 參數，提供您在建立應用程式時所使用的物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="98864-131">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="98864-132">執行此命令之前，您必須允許一些時間讓新的服務主體在整個 Azure Active Directory 中傳播。</span><span class="sxs-lookup"><span data-stu-id="98864-132">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="98864-133">當您手動執行這些命令時，通常工作與工作之間經過的時間已足夠。</span><span class="sxs-lookup"><span data-stu-id="98864-133">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="98864-134">您應該在指令碼中的命令之間加入睡眠步驟 (例如`sleep 15`)。</span><span class="sxs-lookup"><span data-stu-id="98864-134">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="98864-135">如果您看到主體不存在於目錄中的錯誤訊息，請重新執行命令。</span><span class="sxs-lookup"><span data-stu-id="98864-135">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="98864-136">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="98864-136">That's it!</span></span> <span data-ttu-id="98864-137">您的 AD 應用程式和服務主體已設定好。</span><span class="sxs-lookup"><span data-stu-id="98864-137">Your AD application and service principal are set up.</span></span> <span data-ttu-id="98864-138">下一節會說明如何透過 Azure CLI 以認證來登入。</span><span class="sxs-lookup"><span data-stu-id="98864-138">The next section shows you how to log in with the credential through Azure CLI.</span></span> <span data-ttu-id="98864-139">如果您想要在您的程式碼應用程式中使用認證，則不需要繼續進行本主題。</span><span class="sxs-lookup"><span data-stu-id="98864-139">If you want to use the credential in your code application, you do not need to continue with this topic.</span></span> <span data-ttu-id="98864-140">您可以跳到 [範例應用程式](#sample-applications) ，以查看使用應用程式識別碼和密碼來登入的範例。</span><span class="sxs-lookup"><span data-stu-id="98864-140">You can jump to the [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="98864-141">透過 Azure CLI 提供認證</span><span class="sxs-lookup"><span data-stu-id="98864-141">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="98864-142">現在，您需要以應用程式的形式登入以執行作業。</span><span class="sxs-lookup"><span data-stu-id="98864-142">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="98864-143">每當您以服務主體的形式登入時，都需要提供 AD 應用程式目錄的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="98864-143">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="98864-144">租用戶是 Azure Active Directory 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="98864-144">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="98864-145">若要擷取目前已驗證訂用帳戶的租用戶識別碼，請使用︰</span><span class="sxs-lookup"><span data-stu-id="98864-145">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="98864-146">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="98864-146">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="98864-147">如果您需要取得其他訂用帳戶的租用戶識別碼，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="98864-147">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="98864-148">如果您需要擷取用戶端識別碼以便用於登入，請使用︰</span><span class="sxs-lookup"><span data-stu-id="98864-148">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="98864-149">要用於登入的值是服務主體名稱中所列出的 GUID。</span><span class="sxs-lookup"><span data-stu-id="98864-149">The value to use for logging in is the guid listed in the service principal names.</span></span>
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. <span data-ttu-id="98864-150">以服務主體的形式登入。</span><span class="sxs-lookup"><span data-stu-id="98864-150">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="98864-151">系統會提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="98864-151">You are prompted for the password.</span></span> <span data-ttu-id="98864-152">提供您建立 AD 應用程式時指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="98864-152">Provide the password you specified when creating the AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="98864-153">您現在已驗證為您所建立之服務主體的服務主體。</span><span class="sxs-lookup"><span data-stu-id="98864-153">You are now authenticated as the service principal for the service principal that you created.</span></span>

<span data-ttu-id="98864-154">或者，您可以從命令列叫用 REST 作業來登入。</span><span class="sxs-lookup"><span data-stu-id="98864-154">Alternatively, you can invoke REST operations from the command line to log in.</span></span> <span data-ttu-id="98864-155">從驗證回應，您可以擷取存取權杖以用於其他作業。</span><span class="sxs-lookup"><span data-stu-id="98864-155">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="98864-156">如需叫用 REST 作業擷取存取權杖的範例，請參閱[產生存取權杖](resource-manager-rest-api.md#generating-an-access-token)。</span><span class="sxs-lookup"><span data-stu-id="98864-156">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="98864-157">使用憑證建立服務主體</span><span class="sxs-lookup"><span data-stu-id="98864-157">Create service principal with certificate</span></span>
<span data-ttu-id="98864-158">在本節中，您會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="98864-158">In this section, you perform the steps to:</span></span>

* <span data-ttu-id="98864-159">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="98864-159">create a self-signed certificate</span></span>
* <span data-ttu-id="98864-160">建立 AD 應用程式 (包含憑證) 和服務主體</span><span class="sxs-lookup"><span data-stu-id="98864-160">create the AD application with the certificate, and the service principal</span></span>
* <span data-ttu-id="98864-161">將 [讀取者角色] 指派給服務主體</span><span class="sxs-lookup"><span data-stu-id="98864-161">assign the Reader role to the service principal</span></span>

<span data-ttu-id="98864-162">若要完成這些步驟，您必須安裝 [OpenSSL](http://www.openssl.org/) 。</span><span class="sxs-lookup"><span data-stu-id="98864-162">To complete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="98864-163">建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="98864-163">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="98864-164">上一個步驟建立了兩個檔案 - privkey.pem 和 cert.pem。</span><span class="sxs-lookup"><span data-stu-id="98864-164">The preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="98864-165">將公開和私密金鑰結合為單一檔案。</span><span class="sxs-lookup"><span data-stu-id="98864-165">Combine the public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="98864-166">開啟 **examplecert.pem** 檔案並尋找在 **-----BEGIN CERTIFICATE-----** 與 **-----END CERTIFICATE-----** 之間的一長串字元。</span><span class="sxs-lookup"><span data-stu-id="98864-166">Open the **examplecert.pem** file and look for the long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="98864-167">複製憑證資料。</span><span class="sxs-lookup"><span data-stu-id="98864-167">Copy the certificate data.</span></span> <span data-ttu-id="98864-168">您會在建立服務主體時將此資料當作參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="98864-168">You pass this data as a parameter when creating the service principal.</span></span>

4. <span data-ttu-id="98864-169">登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="98864-169">Sign in to your account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="98864-170">若要建立服務主體，請提供應用程式名稱和憑證資料，如下列命令所示︰</span><span class="sxs-lookup"><span data-stu-id="98864-170">To create the service principal, provide the name of the app and the certificate data, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="98864-171">傳回新的服務主體。</span><span class="sxs-lookup"><span data-stu-id="98864-171">The new service principal is returned.</span></span> <span data-ttu-id="98864-172">授與權限時，需要物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="98864-172">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="98864-173">在登入時，則需要隨服務主體名稱列出的 GUID。</span><span class="sxs-lookup"><span data-stu-id="98864-173">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="98864-174">此 GUID 是和應用程式識別碼相同的值。</span><span class="sxs-lookup"><span data-stu-id="98864-174">This guid is the same value as the app id.</span></span> <span data-ttu-id="98864-175">在範例應用程式中，這個值稱為用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="98864-175">In the sample applications, this value is referred to as the Client ID.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. <span data-ttu-id="98864-176">授與服務主體對您訂用帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="98864-176">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="98864-177">在此範例中，您會將服務主體新增至「讀取者」角色，以授與讀取訂用帳戶中所有資源的權限。</span><span class="sxs-lookup"><span data-stu-id="98864-177">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="98864-178">若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="98864-178">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="98864-179">針對 objectid 參數，提供您在建立應用程式時所使用的物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="98864-179">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="98864-180">執行此命令之前，您必須允許一些時間讓新的服務主體在整個 Azure Active Directory 中傳播。</span><span class="sxs-lookup"><span data-stu-id="98864-180">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="98864-181">當您手動執行這些命令時，通常工作與工作之間經過的時間已足夠。</span><span class="sxs-lookup"><span data-stu-id="98864-181">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="98864-182">您應該在指令碼中的命令之間加入睡眠步驟 (例如`sleep 15`)。</span><span class="sxs-lookup"><span data-stu-id="98864-182">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="98864-183">如果您看到主體不存在於目錄中的錯誤訊息，請重新執行命令。</span><span class="sxs-lookup"><span data-stu-id="98864-183">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="98864-184">透過自動化的 Azure CLI 指令碼提供憑證</span><span class="sxs-lookup"><span data-stu-id="98864-184">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="98864-185">現在，您需要以應用程式的形式登入以執行作業。</span><span class="sxs-lookup"><span data-stu-id="98864-185">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="98864-186">每當您以服務主體的形式登入時，都需要提供 AD 應用程式目錄的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="98864-186">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="98864-187">租用戶是 Azure Active Directory 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="98864-187">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="98864-188">若要擷取目前已驗證訂用帳戶的租用戶識別碼，請使用︰</span><span class="sxs-lookup"><span data-stu-id="98864-188">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="98864-189">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="98864-189">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="98864-190">如果您需要取得其他訂用帳戶的租用戶識別碼，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="98864-190">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="98864-191">若要擷取憑證指紋，然後移除不必要的字元，請使用：</span><span class="sxs-lookup"><span data-stu-id="98864-191">To retrieve the certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="98864-192">這會傳回指紋值，類似：</span><span class="sxs-lookup"><span data-stu-id="98864-192">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="98864-193">如果您需要擷取用戶端識別碼以便用於登入，請使用︰</span><span class="sxs-lookup"><span data-stu-id="98864-193">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="98864-194">要用於登入的值是服務主體名稱中所列出的 GUID。</span><span class="sxs-lookup"><span data-stu-id="98864-194">The value to use for logging in is the guid listed in the service principal names.</span></span>
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. <span data-ttu-id="98864-195">以服務主體的形式登入。</span><span class="sxs-lookup"><span data-stu-id="98864-195">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="98864-196">您現在驗證為您所建立之 Azure Active Directory 應用程式的服務主體。</span><span class="sxs-lookup"><span data-stu-id="98864-196">You are now authenticated as the service principal for the Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="98864-197">管理認證</span><span class="sxs-lookup"><span data-stu-id="98864-197">Change credentials</span></span>

<span data-ttu-id="98864-198">若要變更 AD 應用程式認證，不管是因為安全性危害或認證過期，請使用`azure ad app set`。</span><span class="sxs-lookup"><span data-stu-id="98864-198">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="98864-199">若要變更密碼，使用：</span><span class="sxs-lookup"><span data-stu-id="98864-199">To change a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="98864-200">若要變更憑證值，使用︰</span><span class="sxs-lookup"><span data-stu-id="98864-200">To change a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="98864-201">偵錯</span><span class="sxs-lookup"><span data-stu-id="98864-201">Debug</span></span>

<span data-ttu-id="98864-202">建立服務主體時，您可能會遇到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="98864-202">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="98864-203">**Authentication_Unauthorized」**或**「在內容中找不到訂用帳戶。」**</span><span class="sxs-lookup"><span data-stu-id="98864-203">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="98864-204">- 當您的帳戶在 Azure Active Directory 上未具備註冊應用程式的[必要權限](#required-permissions)時，您就會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="98864-204">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="98864-205">通常，只有 Azure Active Directory 中的管理使用者可以註冊應用程式，且您的帳戶不是系統管理員時，就會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="98864-205">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="98864-206">要求系統管理員將您指派給系統管理員角色，或是讓使用者註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="98864-206">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="98864-207">您的帳戶**「沒有在範圍 '/subscriptions/{guid}' 中執行 'Microsoft.Authorization/roleAssignments/write' 動作的權限。」** - 當您的帳戶沒有足夠權限可將角色指派給身分識別時，您就會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="98864-207">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="98864-208">要求訂用帳戶管理員將您新增至「使用者存取系統管理員」角色。</span><span class="sxs-lookup"><span data-stu-id="98864-208">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="98864-209">範例應用程式</span><span class="sxs-lookup"><span data-stu-id="98864-209">Sample applications</span></span>
<span data-ttu-id="98864-210">如需透過不同平台以應用程式身分登入的資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="98864-210">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="98864-211">.NET</span><span class="sxs-lookup"><span data-stu-id="98864-211">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="98864-212">Java</span><span class="sxs-lookup"><span data-stu-id="98864-212">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="98864-213">Node.js</span><span class="sxs-lookup"><span data-stu-id="98864-213">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="98864-214">Python</span><span class="sxs-lookup"><span data-stu-id="98864-214">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="98864-215">Ruby</span><span class="sxs-lookup"><span data-stu-id="98864-215">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="98864-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98864-216">Next steps</span></span>
* <span data-ttu-id="98864-217">如需有關將應用程式整合至 Azure 來管理資源的詳細步驟，請參閱 [利用 Azure Resource Manager API 進行授權的開發人員指南](resource-manager-api-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="98864-217">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="98864-218">如需使用憑證和 Azure CLI 的詳細資訊，請參閱 [從 Linux 命令列以憑證方式驗證 Azure 服務主體](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx)。</span><span class="sxs-lookup"><span data-stu-id="98864-218">To get more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="98864-219">如需可授與或拒絕使用者的可用動作清單，請參閱 [Azure Resource Manager 資源提供者作業](../active-directory/role-based-access-control-resource-provider-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="98864-219">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
