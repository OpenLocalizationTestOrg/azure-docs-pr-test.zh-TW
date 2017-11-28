---
title: "Azure 應用程式使用 Azure CLI aaaCreate 識別 |Microsoft 文件"
description: "描述如何 toouse Azure CLI toocreate Azure Active Directory 應用程式和服務主體授與它存取 tooresources 透過以角色為基礎的存取控制。 它會顯示如何使用密碼或憑證 tooauthenticate 應用程式。"
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
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="de856-104">使用 Azure CLI toocreate 服務主體 tooaccess 資源</span><span class="sxs-lookup"><span data-stu-id="de856-104">Use Azure CLI toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="de856-105">當您擁有的應用程式或需要 tooaccess 資源的指令碼時，您可以設定 hello 應用程式的身分識別，並驗證它自己的認證與 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="de856-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="de856-106">此身分識別就是所謂的服務主體。</span><span class="sxs-lookup"><span data-stu-id="de856-106">This identity is known as a service principal.</span></span> <span data-ttu-id="de856-107">這種方法可讓您︰</span><span class="sxs-lookup"><span data-stu-id="de856-107">This approach enables you to:</span></span>

* <span data-ttu-id="de856-108">指派權限 toohello 不同於您自己的權限的應用程式識別。</span><span class="sxs-lookup"><span data-stu-id="de856-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="de856-109">一般而言，這些權限會限制的 tooexactly 哪些 hello 應用程式需要 toodo。</span><span class="sxs-lookup"><span data-stu-id="de856-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="de856-110">使用憑證在執行無人看管的指令碼時進行驗證。</span><span class="sxs-lookup"><span data-stu-id="de856-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="de856-111">本文章將示範如何 toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset 組成的應用程式 toorun 在它自己的認證和身分識別。</span><span class="sxs-lookup"><span data-stu-id="de856-111">This article shows you how toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset up an application toorun under its own credentials and identity.</span></span> <span data-ttu-id="de856-112">安裝新版的 hello [Azure CLI 1.0](../cli-install-nodejs.md) toomake 確定您的環境符合本文章中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="de856-112">Install hello latest version of [Azure CLI 1.0](../cli-install-nodejs.md) toomake sure your environment matches hello examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="de856-113">所需的權限</span><span class="sxs-lookup"><span data-stu-id="de856-113">Required permissions</span></span>
<span data-ttu-id="de856-114">toocomplete 本主題中，您必須在您的 Azure Active Directory 和 Azure 訂用帳戶擁有足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="de856-114">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="de856-115">具體來說，您必須是能夠 toocreate hello Azure Active Directory 中的應用程式，並且將 hello 服務主體 tooa 角色指派。</span><span class="sxs-lookup"><span data-stu-id="de856-115">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="de856-116">hello 最簡單方式 toocheck 您的帳戶是否有足夠的權限是透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="de856-116">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="de856-117">請參閱[在入口網站中檢查必要的權限](resource-group-create-service-principal-portal.md#required-permissions)。</span><span class="sxs-lookup"><span data-stu-id="de856-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="de856-118">現在，任何繼續 tooa 區段[密碼](#create-service-principal-with-password)或[憑證](#create-service-principal-with-certificate)驗證。</span><span class="sxs-lookup"><span data-stu-id="de856-118">Now, proceed tooa section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="de856-119">使用密碼建立服務主體</span><span class="sxs-lookup"><span data-stu-id="de856-119">Create service principal with password</span></span>
<span data-ttu-id="de856-120">在本節中，您要執行 hello 步驟 toocreate hello 與密碼，AD 應用程式，並指派 hello 讀取器角色 toohello 服務主體。</span><span class="sxs-lookup"><span data-stu-id="de856-120">In this section, you perform hello steps toocreate hello AD application with a password, and assign hello Reader role toohello service principal.</span></span>

1. <span data-ttu-id="de856-121">登入 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="de856-121">Sign in tooyour account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="de856-122">toocreate 一個應用程式的身分識別提供 hello hello 應用程式名稱及密碼，hello 下列命令所示：</span><span class="sxs-lookup"><span data-stu-id="de856-122">toocreate an app identity, provide hello name of hello app and a password, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="de856-123">會傳回 hello 新的服務主體。</span><span class="sxs-lookup"><span data-stu-id="de856-123">hello new service principal is returned.</span></span> <span data-ttu-id="de856-124">授與權限時，就需要物件識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="de856-124">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="de856-125">中的記錄時，就需要 hello guid 與 hello 服務主要名稱一起列出。</span><span class="sxs-lookup"><span data-stu-id="de856-125">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="de856-126">此 guid 為 hello 與 hello 應用程式識別碼相同的值。Hello 範例應用程式中，這個值會為參考的 tooas hello `Client ID`。</span><span class="sxs-lookup"><span data-stu-id="de856-126">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello `Client ID`.</span></span> 
     
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

3. <span data-ttu-id="de856-127">授與 hello 服務主體權限您訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="de856-127">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="de856-128">在此範例中，您可以將 hello 服務主體 toohello 讀取器角色，授與權限 tooread hello 訂用帳戶中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="de856-128">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="de856-129">若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="de856-129">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="de856-130">Hello objectid 參數，提供您建立 hello 應用程式時使用的物件識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="de856-130">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="de856-131">然後再執行此命令，您必須等候一段時間的 hello 新服務主體 toopropagate 整個 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="de856-131">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="de856-132">當您手動執行這些命令時，通常工作與工作之間經過的時間已足夠。</span><span class="sxs-lookup"><span data-stu-id="de856-132">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="de856-133">在指令碼中，您應該加入步驟 toosleep hello 命令之間 (例如`sleep 15`)。</span><span class="sxs-lookup"><span data-stu-id="de856-133">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="de856-134">如果您看到主體的錯誤指出 hello 不存在於 hello 目錄，請重新執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="de856-134">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="de856-135">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="de856-135">That's it!</span></span> <span data-ttu-id="de856-136">您的 AD 應用程式和服務主體已設定好。</span><span class="sxs-lookup"><span data-stu-id="de856-136">Your AD application and service principal are set up.</span></span> <span data-ttu-id="de856-137">hello 下一步 區段會顯示以 hello toolog 透過 Azure CLI 的認證。</span><span class="sxs-lookup"><span data-stu-id="de856-137">hello next section shows you how toolog in with hello credential through Azure CLI.</span></span> <span data-ttu-id="de856-138">如果您想 toouse hello 認證在應用程式程式碼中，您不需要 toocontinue 與這個主題。</span><span class="sxs-lookup"><span data-stu-id="de856-138">If you want toouse hello credential in your code application, you do not need toocontinue with this topic.</span></span> <span data-ttu-id="de856-139">您可以跳 toohello[範例應用程式](#sample-applications)登入您的應用程式識別碼和密碼的範例。</span><span class="sxs-lookup"><span data-stu-id="de856-139">You can jump toohello [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="de856-140">透過 Azure CLI 提供認證</span><span class="sxs-lookup"><span data-stu-id="de856-140">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="de856-141">現在，您必須在 toolog 為 hello tooperform 應用程式的作業。</span><span class="sxs-lookup"><span data-stu-id="de856-141">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="de856-142">每當您登入做為服務主體時，您需要 tooprovide hello 租用戶識別碼 hello 目錄的 AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="de856-142">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="de856-143">租用戶是 Azure Active Directory 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="de856-143">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="de856-144">tooretrieve hello 您目前已驗證的訂閱，使用的租用戶識別碼：</span><span class="sxs-lookup"><span data-stu-id="de856-144">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="de856-145">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="de856-145">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="de856-146">如果您需要 tooget hello 租用戶識別碼的其他訂用帳戶，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="de856-146">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="de856-147">如果您需要 tooretrieve hello 用戶端識別碼 toouse 登入，請使用：</span><span class="sxs-lookup"><span data-stu-id="de856-147">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="de856-148">記錄的 hello 值 toouse 是 hello hello 服務主體名稱中所列的 guid。</span><span class="sxs-lookup"><span data-stu-id="de856-148">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
   
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
3. <span data-ttu-id="de856-149">Hello 服務主體的身分登入。</span><span class="sxs-lookup"><span data-stu-id="de856-149">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="de856-150">系統提示您輸入 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="de856-150">You are prompted for hello password.</span></span> <span data-ttu-id="de856-151">提供建立 hello AD 應用程式時，您所指定的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="de856-151">Provide hello password you specified when creating hello AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="de856-152">您現在會為您建立的 hello 服務主體的 hello 服務主體進行驗證。</span><span class="sxs-lookup"><span data-stu-id="de856-152">You are now authenticated as hello service principal for hello service principal that you created.</span></span>

<span data-ttu-id="de856-153">或者，您可以叫用中的 hello 命令列 toolog 從 REST 作業。</span><span class="sxs-lookup"><span data-stu-id="de856-153">Alternatively, you can invoke REST operations from hello command line toolog in.</span></span> <span data-ttu-id="de856-154">從 hello 驗證回應，您可以擷取 hello 存取權杖用於其他作業。</span><span class="sxs-lookup"><span data-stu-id="de856-154">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="de856-155">藉由叫用 REST 作業擷取 hello 存取權杖的範例，請參閱[產生存取權杖](resource-manager-rest-api.md#generating-an-access-token)。</span><span class="sxs-lookup"><span data-stu-id="de856-155">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="de856-156">使用憑證建立服務主體</span><span class="sxs-lookup"><span data-stu-id="de856-156">Create service principal with certificate</span></span>
<span data-ttu-id="de856-157">在本節中，您可以執行 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="de856-157">In this section, you perform hello steps to:</span></span>

* <span data-ttu-id="de856-158">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="de856-158">create a self-signed certificate</span></span>
* <span data-ttu-id="de856-159">hello 憑證與 hello 服務主體建立 hello AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="de856-159">create hello AD application with hello certificate, and hello service principal</span></span>
* <span data-ttu-id="de856-160">指派 hello 讀取器角色 toohello 服務主體</span><span class="sxs-lookup"><span data-stu-id="de856-160">assign hello Reader role toohello service principal</span></span>

<span data-ttu-id="de856-161">toocomplete 這些步驟，您必須擁有[OpenSSL](http://www.openssl.org/)安裝。</span><span class="sxs-lookup"><span data-stu-id="de856-161">toocomplete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="de856-162">建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="de856-162">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="de856-163">上述步驟建立兩個檔案-privkey.pem 和 cert.pem hello。</span><span class="sxs-lookup"><span data-stu-id="de856-163">hello preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="de856-164">將 hello 公用和私用金鑰結合成單一檔案。</span><span class="sxs-lookup"><span data-stu-id="de856-164">Combine hello public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="de856-165">開啟 hello **examplecert.pem**檔案，並尋找 hello 個之間字元的長串**---BEGIN CERTIFICATE---**和**---憑證結尾---**。</span><span class="sxs-lookup"><span data-stu-id="de856-165">Open hello **examplecert.pem** file and look for hello long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="de856-166">將複製 hello 憑證資料。</span><span class="sxs-lookup"><span data-stu-id="de856-166">Copy hello certificate data.</span></span> <span data-ttu-id="de856-167">建立 hello 服務主體時，您可以傳遞做為參數的資料。</span><span class="sxs-lookup"><span data-stu-id="de856-167">You pass this data as a parameter when creating hello service principal.</span></span>

4. <span data-ttu-id="de856-168">登入 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="de856-168">Sign in tooyour account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="de856-169">toocreate hello 服務主體，會提供 hello 名稱 hello 應用程式和 hello 憑證資料，hello 下列命令所示：</span><span class="sxs-lookup"><span data-stu-id="de856-169">toocreate hello service principal, provide hello name of hello app and hello certificate data, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="de856-170">會傳回 hello 新的服務主體。</span><span class="sxs-lookup"><span data-stu-id="de856-170">hello new service principal is returned.</span></span> <span data-ttu-id="de856-171">授與權限時，就需要物件識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="de856-171">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="de856-172">中的記錄時，就需要 hello guid 與 hello 服務主要名稱一起列出。</span><span class="sxs-lookup"><span data-stu-id="de856-172">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="de856-173">此 guid 為 hello 與 hello 應用程式識別碼相同的值。Hello 範例應用程式中，這個值會為參考的 tooas hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="de856-173">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello Client ID.</span></span> 
     
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
6. <span data-ttu-id="de856-174">授與 hello 服務主體權限您訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="de856-174">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="de856-175">在此範例中，您可以將 hello 服務主體 toohello 讀取器角色，授與權限 tooread hello 訂用帳戶中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="de856-175">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="de856-176">若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="de856-176">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="de856-177">Hello objectid 參數，提供您建立 hello 應用程式時使用的物件識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="de856-177">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="de856-178">然後再執行此命令，您必須等候一段時間的 hello 新服務主體 toopropagate 整個 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="de856-178">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="de856-179">當您手動執行這些命令時，通常工作與工作之間經過的時間已足夠。</span><span class="sxs-lookup"><span data-stu-id="de856-179">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="de856-180">在指令碼中，您應該加入步驟 toosleep hello 命令之間 (例如`sleep 15`)。</span><span class="sxs-lookup"><span data-stu-id="de856-180">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="de856-181">如果您看到主體的錯誤指出 hello 不存在於 hello 目錄，請重新執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="de856-181">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="de856-182">透過自動化的 Azure CLI 指令碼提供憑證</span><span class="sxs-lookup"><span data-stu-id="de856-182">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="de856-183">現在，您必須在 toolog 為 hello tooperform 應用程式的作業。</span><span class="sxs-lookup"><span data-stu-id="de856-183">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="de856-184">每當您登入做為服務主體時，您需要 tooprovide hello 租用戶識別碼 hello 目錄的 AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="de856-184">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="de856-185">租用戶是 Azure Active Directory 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="de856-185">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="de856-186">tooretrieve hello 您目前已驗證的訂閱，使用的租用戶識別碼：</span><span class="sxs-lookup"><span data-stu-id="de856-186">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="de856-187">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="de856-187">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="de856-188">如果您需要 tooget hello 租用戶識別碼的其他訂用帳戶，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="de856-188">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="de856-189">tooretrieve hello 憑證指紋和移除不必要的字元，請使用：</span><span class="sxs-lookup"><span data-stu-id="de856-189">tooretrieve hello certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="de856-190">這會傳回指紋值，類似：</span><span class="sxs-lookup"><span data-stu-id="de856-190">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="de856-191">如果您需要 tooretrieve hello 用戶端識別碼 toouse 登入，請使用：</span><span class="sxs-lookup"><span data-stu-id="de856-191">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="de856-192">記錄的 hello 值 toouse 是 hello hello 服務主體名稱中所列的 guid。</span><span class="sxs-lookup"><span data-stu-id="de856-192">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
     
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
4. <span data-ttu-id="de856-193">Hello 服務主體的身分登入。</span><span class="sxs-lookup"><span data-stu-id="de856-193">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="de856-194">您現在會做為 hello hello 您建立的 Azure Active Directory 應用程式之主體的服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="de856-194">You are now authenticated as hello service principal for hello Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="de856-195">管理認證</span><span class="sxs-lookup"><span data-stu-id="de856-195">Change credentials</span></span>

<span data-ttu-id="de856-196">AD 應用程式，因為安全性洩露或認證過期的 toochange hello 認證使用`azure ad app set`。</span><span class="sxs-lookup"><span data-stu-id="de856-196">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="de856-197">toochange 密碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="de856-197">toochange a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="de856-198">toochange 憑證的值，請使用：</span><span class="sxs-lookup"><span data-stu-id="de856-198">toochange a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="de856-199">偵錯</span><span class="sxs-lookup"><span data-stu-id="de856-199">Debug</span></span>

<span data-ttu-id="de856-200">您可能會遇到下列錯誤，建立服務主體時的 hello:</span><span class="sxs-lookup"><span data-stu-id="de856-200">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="de856-201">**「 Authentication_Unauthorized"**或**」 沒有訂用帳戶中找到 hello 內容。 」**</span><span class="sxs-lookup"><span data-stu-id="de856-201">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="de856-202">-您會看到這個錯誤，當您的帳戶未具備 hello[必要的權限](#required-permissions)hello Azure Active Directory tooregister 應用程式上。</span><span class="sxs-lookup"><span data-stu-id="de856-202">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="de856-203">通常，只有 Azure Active Directory 中的管理使用者可以註冊應用程式，且您的帳戶不是系統管理員時，就會看到此錯誤。請要求系統管理員 tooeither 指派您 tooan 系統管理員角色或 tooenable 使用者 tooregister 應用程式。</span><span class="sxs-lookup"><span data-stu-id="de856-203">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="de856-204">您的帳戶**」 沒有授權 tooperform 動作 'Microsoft.Authorization/roleAssignments/write' 對範圍 ' / 訂用帳戶 / {guid}'。 」** -當您的帳戶未具備足夠的權限 tooassign 角色 tooan 身分識別，您會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="de856-204">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="de856-205">詢問您的訂用帳戶管理員 tooadd 您 tooUser 存取 」 系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="de856-205">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="de856-206">範例應用程式</span><span class="sxs-lookup"><span data-stu-id="de856-206">Sample applications</span></span>
<span data-ttu-id="de856-207">如需透過不同平台的 hello 應用程式以登入資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="de856-207">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="de856-208">.NET</span><span class="sxs-lookup"><span data-stu-id="de856-208">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="de856-209">Java</span><span class="sxs-lookup"><span data-stu-id="de856-209">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="de856-210">Node.js</span><span class="sxs-lookup"><span data-stu-id="de856-210">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="de856-211">Python</span><span class="sxs-lookup"><span data-stu-id="de856-211">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="de856-212">Ruby</span><span class="sxs-lookup"><span data-stu-id="de856-212">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="de856-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="de856-213">Next steps</span></span>
* <span data-ttu-id="de856-214">如需整合到 Azure 的應用程式管理資源的詳細步驟，請參閱[以 hello Azure 資源管理員 API 的開發人員指南 tooauthorization](resource-manager-api-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="de856-214">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="de856-215">tooget 需使用憑證和 Azure CLI，請參閱[憑證型驗證的 Azure 服務主體使用 Linux 命令列從](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx)。</span><span class="sxs-lookup"><span data-stu-id="de856-215">tooget more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="de856-216">如需可授與或拒絕 toousers 可用動作的清單，請參閱[Azure 資源管理員資源提供者作業](../active-directory/role-based-access-control-resource-provider-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="de856-216">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
