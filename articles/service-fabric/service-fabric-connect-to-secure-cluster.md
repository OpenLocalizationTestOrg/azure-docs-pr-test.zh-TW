---
title: "以安全的方式連線到 Azure Service Fabric 叢集 | Microsoft Docs"
description: "說明如何驗證用戶端對 Service Fabric 叢集的存取，以及如何保護用戶端與叢集之間的通訊。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 759a539e-e5e6-4055-bff5-d38804656e10
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: d6a13ceb8ccd9207ecacc166247535d496d5dec7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="ebcd7-103">連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-103">Connect to a secure cluster</span></span>

<span data-ttu-id="ebcd7-104">當用戶端連線到 Service Fabric 叢集節點時，用戶端可以使用憑證安全性或 Azure Active Directory (AAD) 來接受驗證及保護已建立的通訊。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-104">When a client connects to a Service Fabric cluster node, the client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="ebcd7-105">此驗證可確保只有已獲授權的使用者可以存取叢集和已部署的應用程式，以及執行管理工作。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-105">This authentication ensures that only authorized users can access the cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="ebcd7-106">憑證或 AAD 安全性必須在叢集建立之時即事先在叢集上啟用。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-106">Certificate or AAD security must have been previously enabled on the cluster when the cluster was created.</span></span>  <span data-ttu-id="ebcd7-107">如需有關叢集安全性案例的詳細資訊，請參閱 [叢集安全性](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="ebcd7-108">如果您要連接到使用憑證保護的叢集，請在要連接到叢集的電腦上[設定用戶端憑證](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert)。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-108">If you are connecting to a cluster secured with certificates, [set up the client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on the computer that connects to the cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-to-a-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="ebcd7-109">使用 Azure Service Fabric CLI (sfctl) 連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-109">Connect to a secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="ebcd7-110">有幾個不同的方式可使用 Service Fabric CLI (sfctl) 來連線到安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-110">There are a few different ways to connect to a secure cluster using the Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="ebcd7-111">使用用戶端憑證來進行驗證時，憑證詳細資料必須與部署至叢集節點的憑證相符。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-111">When using a client certificate for authentication, the certificate details must match a certificate deployed to the cluster nodes.</span></span> <span data-ttu-id="ebcd7-112">如果您的憑證有「憑證授權單位」(CA)，就必須額外指定信任的 CA。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-112">If your certificate has Certificate Authorities (CAs), you need to additionally specify the trusted CAs.</span></span>

<span data-ttu-id="ebcd7-113">您可以使用 `sfctl cluster select` 命令來連線到叢集。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-113">You can connect to a cluster using the `sfctl cluster select` command.</span></span>

<span data-ttu-id="ebcd7-114">指定用戶端憑證時，可以使用兩種不同的方式，以憑證與金鑰組方式指定，或是以單一 pem 檔案方式指定。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="ebcd7-115">針對受密碼保護的 `pem` 檔案，系統會自動提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-115">For password protected `pem` files, you will be prompted automatically to enter the password.</span></span>

<span data-ttu-id="ebcd7-116">若要以 pem 檔案指定用戶端憑證，請在 `--pem` 引數中指定檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-116">To specify the client certificate as a pem file, specify the file path in the `--pem` argument.</span></span> <span data-ttu-id="ebcd7-117">例如：</span><span class="sxs-lookup"><span data-stu-id="ebcd7-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="ebcd7-118">受密碼保護的 pem 檔案會在執行任何命令之前，先提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-118">Password protected pem files will prompt for password prior to running any command.</span></span>

<span data-ttu-id="ebcd7-119">為了指定憑證，金鑰組會使用 `--cert` 和 `--key` 引數來指定每個個別檔案的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-119">To specify a cert, key pair use the `--cert` and `--key` arguments to specify the file paths to each respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="ebcd7-120">有時，用來保護測試或開發叢集的憑證會讓憑證驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-120">Sometimes certificates used to secure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="ebcd7-121">若要略過憑證驗證，請指定 `--no-verify` 選項。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-121">To bypass certificate verification, specify the `--no-verify` option.</span></span> <span data-ttu-id="ebcd7-122">例如：</span><span class="sxs-lookup"><span data-stu-id="ebcd7-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="ebcd7-123">連線到生產環境 Service Fabric 叢集時，請勿使用 `no-verify` 選項。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-123">Do not use the `no-verify` option when connecting to production Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="ebcd7-124">此外，您可以指定受信任 CA 憑證，或個別憑證的目錄路徑。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-124">In addition, you can specify paths to directories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="ebcd7-125">若要指定這些路徑，請使用 `--ca` 引數。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-125">To specify these paths, use the `--ca` argument.</span></span> <span data-ttu-id="ebcd7-126">例如：</span><span class="sxs-lookup"><span data-stu-id="ebcd7-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="ebcd7-127">連線之後，您應該能夠[執行其他 sfctl 命令](service-fabric-cli.md)來與叢集互動。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-127">After you connect, you should be able to [run other sfctl commands](service-fabric-cli.md) to interact with the cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-to-a-cluster-using-powershell"></a><span data-ttu-id="ebcd7-128">使用 PowerShell 來連線到叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-128">Connect to a cluster using PowerShell</span></span>
<span data-ttu-id="ebcd7-129">在您透過 PowerShell 執行叢集上的作業之前，先建立叢集的連接。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-129">Before you perform operations on a cluster through PowerShell, first establish a connection to the cluster.</span></span> <span data-ttu-id="ebcd7-130">叢集連接適用於指定 PowerShell 工作階段中的所有後續命令。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-130">The cluster connection is used for all subsequent commands in the given PowerShell session.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="ebcd7-131">連線到不安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-131">Connect to an unsecure cluster</span></span>

<span data-ttu-id="ebcd7-132">若要連接至不安全的叢集，請提供叢集端點位址至 **Connect-ServiceFabricCluster** 命令︰</span><span class="sxs-lookup"><span data-stu-id="ebcd7-132">To connect to an unsecure cluster, provide the cluster endpoint address to the **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="ebcd7-133">使用 Azure Active Directory 連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-133">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="ebcd7-134">若要連接至使用 Azure Active Directory 來授權叢集系統管理員存取權的安全叢集，請提供叢集憑證指紋，並使用 AzureActiveDirectory 旗標。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-134">To connect to a secure cluster that uses Azure Active Directory to authorize cluster administrator access, provide the cluster certificate thumbprint and use the *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="ebcd7-135">使用用戶端憑證連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-135">Connect to a secure cluster using a client certificate</span></span>
<span data-ttu-id="ebcd7-136">執行下列 PowerShell 命令來連線至使用用戶端憑證授權系統管理員存取權的安全叢集。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-136">Run the following PowerShell command to connect to a secure cluster that uses client certificates to authorize administrator access.</span></span> <span data-ttu-id="ebcd7-137">提供叢集憑證指紋，以及已授與權限來管理叢集的用戶端憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-137">Provide the cluster certificate thumbprint and the thumbprint of the client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="ebcd7-138">憑證詳細資料必須與叢集節點上的憑證相符。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-138">The certificate details must match a certificate on the cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="ebcd7-139">*ServerCertThumbprint* 是安裝在叢集節點上的伺服器憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-139">*ServerCertThumbprint* is the thumbprint of the server certificate installed on the cluster nodes.</span></span> <span data-ttu-id="ebcd7-140">*FindValue* 是系統管理員用戶端憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-140">*FindValue* is the thumbprint of the admin client certificate.</span></span>
<span data-ttu-id="ebcd7-141">填入參數後，命令看起來如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="ebcd7-141">When the parameters are filled in, the command looks like the following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-to-a-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="ebcd7-142">使用 Windows Active Directory 連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-142">Connect to a secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="ebcd7-143">如果您的獨立叢集是使用 AD 安全性部署，可加上 "WindowsCredential" 參數來連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-143">If your standalone cluster is deployed using AD security, connect to the cluster by appending the switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-to-a-cluster-using-the-fabricclient-apis"></a><span data-ttu-id="ebcd7-144">使用 FabricClient API 來連線到叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-144">Connect to a cluster using the FabricClient APIs</span></span>
<span data-ttu-id="ebcd7-145">Service Fabric SDK 會提供叢集管理的 [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) 類別。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-145">The Service Fabric SDK provides the [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="ebcd7-146">若要使用 FabricClient API，請取得 Microsoft.ServiceFabric NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-146">To use the FabricClient APIs, get the Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="ebcd7-147">連線到不安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-147">Connect to an unsecure cluster</span></span>

<span data-ttu-id="ebcd7-148">若要連接至遠端不安全的叢集，建立 FabricClient 執行個體，並提供叢集位址︰</span><span class="sxs-lookup"><span data-stu-id="ebcd7-148">To connect to a remote unsecured cluster, create a FabricClient instance and provide the cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="ebcd7-149">針對在叢集 (例如，Reliable Service) 內執行的程式碼，建立 FabricClient 且不指定叢集位址。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying the cluster address.</span></span> <span data-ttu-id="ebcd7-150">FabricClient 連接到目前正在執行程式碼之節點上的本機管理閘道，避免額外的網路躍點。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-150">FabricClient connects to the local management gateway on the node the code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="ebcd7-151">使用用戶端憑證連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-151">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="ebcd7-152">叢集中的節點必須具備有效的憑證，這些憑證在 SAN 中的通用名稱或 DNS 名稱會出現在於 [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) 上設定的 [RemoteCommonNames](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) 屬性中。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-152">The nodes in the cluster must have valid certificates whose common name or DNS name in SAN appears in the [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="ebcd7-153">遵循此程序，就可讓用戶端與叢集節點之間進行相互驗證。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-153">Following this process enables mutual authentication between the client and the cluster nodes.</span></span>

```csharp
using System.Fabric;
using System.Security.Cryptography.X509Certificates;

string clientCertThumb = "71DE04467C9ED0544D021098BCD44C71E183414E";
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string CommonName = "www.clustername.westus.azure.com";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var xc = GetCredentials(clientCertThumb, serverCertThumb, CommonName);
var fc = new FabricClient(xc, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

static X509Credentials GetCredentials(string clientCertThumb, string serverCertThumb, string name)
{
    X509Credentials xc = new X509Credentials();
    xc.StoreLocation = StoreLocation.CurrentUser;
    xc.StoreName = "My";
    xc.FindType = X509FindType.FindByThumbprint;
    xc.FindValue = clientCertThumb;
    xc.RemoteCommonNames.Add(name);
    xc.RemoteCertThumbprints.Add(serverCertThumb);
    xc.ProtectionLevel = ProtectionLevel.EncryptAndSign;
    return xc;
}
```

### <a name="connect-to-a-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="ebcd7-154">使用 Azure Active Directory 以互動方式連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-154">Connect to a secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="ebcd7-155">以下範例針對用戶端身分識別使用 Azure Active Directory，以及針對伺服器身分識別啟用伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-155">The following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="ebcd7-156">連線到叢集時，就會自動彈出對話方塊視窗，以供互動式登入。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-156">A dialog window automatically pops up for interactive sign-in upon connecting to the cluster.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}
```

### <a name="connect-to-a-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="ebcd7-157">使用 Azure Active Directory 以非互動方式連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-157">Connect to a secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="ebcd7-158">以下範例依存於 Microsoft.IdentityModel.Clients.ActiveDirectory，版本：2.19.208020213。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-158">The following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="ebcd7-159">如需 AAD 權杖取得的詳細資訊，請參閱 [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

```csharp
string tenantId = "C15CFCEA-02C1-40DC-8466-FBD0EE0B05D2";
string clientApplicationId = "118473C2-7619-46E3-A8E4-6DA8D5F56E12";
string webApplicationId = "53E6948C-0897-4DA6-B26A-EE2A38A690B4";

string token = GetAccessToken(
    tenantId,
    webApplicationId,
    clientApplicationId,
    "urn:ietf:wg:oauth:2.0:oob");

string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);
claimsCredentials.LocalClaims = token;

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(
    string tenantId,
    string resource,
    string clientId,
    string redirectUri)
{
    string authorityFormat = @"https://login.microsoftonline.com/{0}";
    string authority = string.Format(CultureInfo.InvariantCulture, authorityFormat, tenantId);
    var authContext = new AuthenticationContext(authority);

    var authResult = authContext.AcquireToken(
        resource,
        clientId,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

### <a name="connect-to-a-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="ebcd7-160">使用 Azure Active Directory 連線到安全的叢集而不需事先知道中繼資料</span><span class="sxs-lookup"><span data-stu-id="ebcd7-160">Connect to a secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="ebcd7-161">以下範例使用非互動權杖取得，但可以使用同樣的方法來建立自訂的互動式權杖取得經驗。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-161">The following example uses non-interactive token acquisition, but the same approach can be used to build a custom interactive token acquisition experience.</span></span> <span data-ttu-id="ebcd7-162">權杖取得所需的 Azure Active Directory 中繼資料是從叢集設定來讀取。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-162">The Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

fc.ClaimsRetrieval += (o, e) =>
{
    return GetAccessToken(e.AzureActiveDirectoryMetadata);
};

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(AzureActiveDirectoryMetadata aad)
{
    var authContext = new AuthenticationContext(aad.Authority);

    var authResult = authContext.AcquireToken(
        aad.ClusterApplication,
        aad.ClientApplication,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

<a id="connectsecureclustersfx"></a>

## <a name="connect-to-a-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="ebcd7-163">使用 Service Fabric Explorer 連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-163">Connect to a secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="ebcd7-164">若要連線到指定之叢集的 [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)，請將您的瀏覽器指向：</span><span class="sxs-lookup"><span data-stu-id="ebcd7-164">To reach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="ebcd7-165">Azure 入口網站的叢集基本資訊窗格中也會提供完整 URL。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-165">The full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="ebcd7-166">使用 Azure Active Directory 連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-166">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="ebcd7-167">若要連接至使用 AAD 保護的叢集，請將您的瀏覽器指向：</span><span class="sxs-lookup"><span data-stu-id="ebcd7-167">To connect to a cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="ebcd7-168">系統將會自動提示您使用 AAD 登入。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-168">You are automatically be prompted to log in with AAD.</span></span>

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="ebcd7-169">使用用戶端憑證連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ebcd7-169">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="ebcd7-170">若要連接至使用憑證保護的叢集，請將您的瀏覽器指向：</span><span class="sxs-lookup"><span data-stu-id="ebcd7-170">To connect to a cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="ebcd7-171">系統會自動提示您選取用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-171">You are automatically be prompted to select a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-the-remote-computer"></a><span data-ttu-id="ebcd7-172">設定遠端電腦上的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="ebcd7-172">Set up a client certificate on the remote computer</span></span>
<span data-ttu-id="ebcd7-173">至少應使用兩個憑證保護叢集，一個是叢集和伺服器憑證，另一個用於用戶端存取。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-173">At least two certificates should be used for securing the cluster, one for the cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="ebcd7-174">建議您也使用額外的次要憑證和用戶端存取憑證。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="ebcd7-175">若要使用憑證安全性來保護用戶端與叢集節點之間的通訊，您必須先取得並安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-175">To secure the communication between a client and a cluster node using certificate security, you first need to obtain and install the client certificate.</span></span> <span data-ttu-id="ebcd7-176">此憑證可以安裝到本機電腦或目前使用者的個人 (My) 存放區。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-176">The certificate can be installed into the Personal (My) store of the local computer or the current user.</span></span>  <span data-ttu-id="ebcd7-177">您也需要伺服器憑證的指紋，讓用戶端可以驗證叢集。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-177">You also need the thumbprint of the server certificate so that the client can authenticate the cluster.</span></span>

<span data-ttu-id="ebcd7-178">請執行下列 PowerShell Cmdlet 以在您存取叢集的電腦上設定用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-178">Run the following PowerShell cmdlet to set up the client certificate on the computer from which you access the cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="ebcd7-179">如果是自我簽署憑證，您必須先把它匯入您電腦的「受信任的人」存放區，才能使用此憑證來連線到安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="ebcd7-179">If it is a self-signed certificate, you need to import it to your machine's "trusted people" store before you can use this certificate to connect to a secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="ebcd7-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ebcd7-180">Next steps</span></span>

* [<span data-ttu-id="ebcd7-181">Service Fabric 叢集升級程序與您的期望</span><span class="sxs-lookup"><span data-stu-id="ebcd7-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="ebcd7-182">在 Visual Studio 中管理 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="ebcd7-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="ebcd7-183">Service Fabric 健康情況模型簡介</span><span class="sxs-lookup"><span data-stu-id="ebcd7-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="ebcd7-184">應用程式安全性及 RunAs</span><span class="sxs-lookup"><span data-stu-id="ebcd7-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="ebcd7-185">開始使用 Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="ebcd7-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
