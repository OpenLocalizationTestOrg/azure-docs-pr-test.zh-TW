---
title: "aaaConnect 安全地 tooan Azure Service Fabric 叢集 |Microsoft 文件"
description: "說明如何 tooauthenticate 用戶端存取 tooa Service Fabric 叢集以及如何 toosecure 用戶端和一個叢集之間的通訊。"
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
ms.openlocfilehash: 1b6a87a1fefaddce2043c604ca53751157232170
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-cluster"></a>Tooa 安全叢集連線

當用戶端連線 tooa Service Fabric 叢集節點時，hello 用戶端可以使用憑證安全性或 Azure Active Directory (AAD) 來建立已驗證且安全之通訊。 此驗證可確保只有授權的使用者可以存取 hello 叢集和部署的應用程式，以及執行管理工作。  憑證或 AAD 安全性群組必須先前啟用 hello 叢集上建立 hello 叢集時。  如需有關叢集安全性案例的詳細資訊，請參閱 [叢集安全性](service-fabric-cluster-security.md)。 如果您要連接的憑證，以保護 tooa 叢集[設定 hello 用戶端憑證](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert)連接 toohello 群集的 hello 電腦上。 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a>使用 Azure Service Fabric CLI (sfctl) tooa 安全叢集連線

有幾個不同的方式 tooconnect tooa 安全使用叢集 hello 服務網狀架構 CLI (sfctl)。 當使用用戶端憑證進行驗證，hello 憑證詳細資料必須符合憑證會部署 toohello 叢集節點。 如果您的憑證的憑證授權單位 (Ca)，您需要 tooadditionally 指定 hello 信任的 Ca。

您可以連接使用 hello tooa 叢集`sfctl cluster select`命令。

指定用戶端憑證時，可以使用兩種不同的方式，以憑證與金鑰組方式指定，或是以單一 pem 檔案方式指定。 針對受密碼保護`pem`檔案，您將會自動提示 tooenter hello 密碼。

toospecify hello 用戶端憑證，為 pem 檔案，請指定 hello 檔案路徑中 hello`--pem`引數。 例如：

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

密碼保護的 pem 檔案會提示輸入密碼之前 toorunning 任何命令。

toospecify 憑證、 金鑰組使用 hello`--cert`和`--key`toospecify hello 檔案路徑 tooeach 個別檔案的引數。

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

憑證有時用 toosecure 測試或開發人員叢集憑證驗證失敗。 toobypass 憑證驗證，指定 hello`--no-verify`選項。 例如：

> [!WARNING]
> 請勿使用 hello`no-verify`選項連接 tooproduction Service Fabric 叢集時。

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

此外，您可以指定路徑 toodirectories 的受信任的 CA 憑證或個別的憑證。 toospecify 這些路徑中，使用 hello`--ca`引數。 例如：

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

您連接之後，您應該會太[執行其他 sfctl 命令](service-fabric-cli.md)toointeract 與 hello 叢集。

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a>Tooa 叢集使用 PowerShell 連線
您透過 PowerShell 的叢集上執行作業之前，先建立連接 toohello 叢集。 hello 叢集連線用於 hello 提供 PowerShell 工作階段中的所有後續命令。

### <a name="connect-tooan-unsecure-cluster"></a>Tooan 不安全叢集連線

tooconnect tooan 不安全叢集時，提供 hello 叢集端點位址 toohello **Connect-servicefabriccluster**命令：

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>使用 Azure Active Directory tooa 安全叢集連線

tooconnect tooa 安全叢集使用 Azure Active Directory tooauthorize 叢集系統管理員存取權，提供 hello 叢集的憑證指紋，並使用 hello *AzureActiveDirectory*旗標。  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>使用用戶端憑證的 tooa 安全叢集連線
執行下列 PowerShell 命令 tooconnect tooa 安全叢集的 hello 會使用用戶端憑證 tooauthorize 系統管理員存取權。 提供 hello 叢集憑證指紋和 hello hello 已授與權限來管理叢集的用戶端憑證的指紋。 hello 憑證詳細資料必須符合 hello 叢集節點上的憑證。

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

*ServerCertThumbprint* hello hello hello 叢集節點上安裝的伺服器憑證的指紋。 *FindValue* hello hello 管理用戶端憑證的指紋。
當 hello 參數會因為填滿時，hello 命令看起來類似下列範例中的 hello: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a>使用 Windows Active Directory tooa 安全叢集連線
如果您的獨立叢集部署使用 AD 安全性時，連接 toohello 叢集附加 hello 交換器"WindowsCredential"。

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a>使用 hello FabricClient Api tooa 叢集連線
hello Service Fabric SDK 提供 hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient)叢集管理的類別。 toouse hello FabricClient Api 取得 hello Microsoft.ServiceFabric NuGet 封裝。

### <a name="connect-tooan-unsecure-cluster"></a>Tooan 不安全叢集連線

tooconnect tooa 遠端不安全的叢集建立 FabricClient 的執行個體，並提供 hello 叢集位址：

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

對於來自叢集內執行的程式碼，例如，在可靠的服務中，建立 FabricClient*沒有*指定 hello 叢集位址。 FabricClient 連接 toohello 本機管理 hello 節點 hello 程式碼的閘道器目前正在上執行，避免額外的網路躍點。

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>使用用戶端憑證的 tooa 安全叢集連線

hello hello 叢集中的節點必須具有有效的憑證一般名稱或 SAN 中的 DNS 名稱會出現在 hello [RemoteCommonNames 屬性](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames)上設定[FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient)。 此程序來啟用 hello 用戶端與 hello 叢集節點之間的相互驗證。

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

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a>以互動方式使用 Azure Active Directory tooa 安全叢集連線

下列範例會使用 Azure Active Directory 伺服器身分識別的用戶端身分識別與伺服器憑證的 hello。

對話方塊視窗會自動快顯互動式登入連線 toohello 叢集時。

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

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a>非互動方式使用 Azure Active Directory tooa 安全叢集連線

hello 下例依賴 Microsoft.IdentityModel.Clients.ActiveDirectory，版本： 2.19.208020213。

如需 AAD 權杖取得的詳細資訊，請參閱 [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx)。

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

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a>使用 Azure Active Directory 的先前的中繼資料不知情的情況下連接 tooa 安全叢集

hello 下列範例會使用非互動式權杖取得，但是 hello 相同的方法可以使用的 toobuild 自訂的互動式權杖取得體驗。 hello 權杖取得所需的 Azure Active Directory 中繼資料會從叢集設定中讀取。

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

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a>使用 Service Fabric 總管 tooa 安全叢集連線
tooreach [Service Fabric 總管](service-fabric-visualizing-your-cluster.md)指定叢集中，會指向您的瀏覽器：

`http://<your-cluster-endpoint>:19080/Explorer`

hello 完整的 URL 也會提供 hello 叢集 essentials 窗格中的 hello Azure 入口網站。

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>使用 Azure Active Directory tooa 安全叢集連線

tooconnect tooa 叢集則受到 AAD，指向您的瀏覽器：

`https://<your-cluster-endpoint>:19080/Explorer`

使用 AAD 提示的 toolog 是可以自動。

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>使用用戶端憑證的 tooa 安全叢集連線

tooconnect tooa 叢集保護憑證，來指向您的瀏覽器：

`https://<your-cluster-endpoint>:19080/Explorer`

您會自動是提示的 tooselect 用戶端憑證。

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a>設定 hello 遠端電腦上的用戶端憑證
兩個以上的憑證應該用於保護 hello 叢集，一個用於 hello 叢集和伺服器憑證，另一個用於用戶端存取。  建議您也使用額外的次要憑證和用戶端存取憑證。  toosecure hello 來進行通訊之用戶端和叢集節點，使用憑證的安全性，首先需要 tooobtain 並安裝 hello 用戶端憑證。 hello 憑證可以安裝到 hello 個人 (My) 存放區的 hello 本機電腦或 hello 目前的使用者。  您也需要 hello hello 伺服器憑證的指紋，以便 hello 用戶端可以驗證 hello 叢集。

執行下列 PowerShell 指令程式 tooset hello hello 電腦，您可以從中存取 hello 叢集上的用戶端憑證的 hello。

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

如果是自我簽署的憑證，您會需要的 tooimport 它 tooyour 機器的 「 受信任的人 」 存放區才能使用此憑證 tooconnect tooa 安全叢集。

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a>後續步驟

* [Service Fabric 叢集升級程序與您的期望](service-fabric-cluster-upgrade.md)
* [在 Visual Studio 中管理 Service Fabric 應用程式](service-fabric-manage-application-in-visual-studio.md)
* [Service Fabric 健康情況模型簡介](service-fabric-health-introduction.md)
* [應用程式安全性及 RunAs](service-fabric-application-runas-security.md)
* [開始使用 Service Fabric CLI](service-fabric-cli.md)
