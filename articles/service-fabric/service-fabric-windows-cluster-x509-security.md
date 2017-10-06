---
title: "aaaSecure Azure Service Fabric 叢集使用的憑證在 Windows 上 |Microsoft 文件"
description: "本文說明 toosecure 通訊內 hello 獨立或私用叢集以及的用戶端與 hello 叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>使用 X.509 憑證保護 Windows 上的獨立叢集
本文說明如何 toosecure hello 溝通 hello 獨立 Windows 叢集的不同節點，以及如何 tooauthenticate 連接的用戶端 toothis 叢集會使用 X.509 憑證。 這樣可以確保，只有授權的使用者可以存取 hello 叢集 hello 部署之應用程式執行管理工作。  建立 hello 叢集時，應該 hello 叢集上啟用憑證安全性。  

如需諸如節點對節點安全性、用戶端對節點安全性、角色型存取控制等有關叢集安全性的詳細資訊，請參閱 [叢集安全性案例](service-fabric-cluster-security.md)。

## <a name="which-certificates-will-you-need"></a>您需要哪些憑證？
toostart，[下載 hello 獨立叢集封裝](service-fabric-cluster-creation-for-windows-server.md#downloadpackage)tooone 的 hello 叢集中的節點。 在 hello 下載封裝，您會發現**ClusterConfig.X509.MultiMachine.json**檔案。 開啟 hello 檔案，並檢閱 hello 區段**安全性**下 hello**屬性**> 一節：

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

本章節描述您需要為保護您的獨立 Windows 叢集的 hello 憑證。 如果您指定叢集憑證時，設定 hello 值**ClusterCredentialType** too_**X509**_。如果您指定的外部連接的伺服器憑證時，設定 hello **ServerCredentialType**太_**X509**_。雖然並非必要，但建議 toohave 正確安全叢集的兩個這些憑證。如果這些值設定得*X509*接著，您也必須指定 hello 對應憑證或服務的網狀架構將會擲回例外狀況。在某些情況下，您可能只想 toospecify hello _ClientCertificateThumbprints_或_ReverseProxyCertificate_。在這些情況下，您需要設定_ClusterCredentialType_或_ServerCredentialType_ too_X509_。


> [!NOTE]
> A[指紋](https://en.wikipedia.org/wiki/Public_key_fingerprint)是 hello 主要身分識別的憑證。 讀取[如何 tooretrieve 憑證的指紋](https://msdn.microsoft.com/library/ms734695.aspx)toofind 出 hello hello 您所建立的憑證指紋。
> 
> 

hello 下表列出您必須在叢集設定的 hello 憑證：

| **CertificateInformation 設定** | **說明** |
| --- | --- |
| ClusterCertificate |建議針對測試環境。 此憑證是在叢集上的 hello 節點之間需要的 toosecure hello 通訊。 您可以使用兩個不同的憑證 (主要和次要) 進行更新。 設定在 hello hello hello 主要憑證指紋**指紋**> 一節，在 hello 次要 hello **ThumbprintSecondary**變數。 |
| ClusterCertificateCommonNames |建議針對生產環境。 此憑證是在叢集上的 hello 節點之間需要的 toosecure hello 通訊。 您可以使用一或兩個叢集憑證通用名稱。 |
| ServerCertificate |建議針對測試環境。 當它嘗試 tooconnect toothis 叢集時，此憑證會呈現 toohello 用戶端。 為了方便起見，您可以選擇 toouse 相同憑證的 hello *ClusterCertificate*和*ServerCertificate*。 您可以使用兩個不同的伺服器憑證 (主要和次要) 進行更新。 設定在 hello hello hello 主要憑證指紋**指紋**> 一節，在 hello 次要 hello **ThumbprintSecondary**變數。 |
| ServerCertificateCommonNames |建議針對生產環境。 當它嘗試 tooconnect toothis 叢集時，此憑證會呈現 toohello 用戶端。 為了方便起見，您可以選擇 toouse 相同憑證的 hello *ClusterCertificateCommonNames*和*ServerCertificateCommonNames*。 您可以使用一或兩個伺服器憑證通用名稱。 |
| ClientCertificateThumbprints |這是一組您想 tooinstall hello 驗證用戶端上的憑證。 您可以有數個不同的用戶端憑證安裝在您想 tooallow 存取 toohello 叢集 hello 機器上。 在 hello 中設定每個憑證的指紋，hello **CertificateThumbprint**變數。 如果您設定 hello **IsAdmin**太*true*，然後 hello 與在其上安裝此憑證的用戶端可以執行系統管理員在 hello 叢集上的管理活動。 如果 hello **IsAdmin**是*false*，hello 與此憑證的用戶端只能執行 hello 動作允許使用者存取權限，通常是唯讀的。 如需角色的詳細資訊，請參閱 [角色型存取控制 (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |設定 hello 的一般名稱的第一個用戶端憑證 hello hello **CertificateCommonName**。 hello **CertificateIssuerThumbprint** hello 指紋為 hello 這個憑證的簽發者。 讀取[使用憑證](https://msdn.microsoft.com/library/ms731899.aspx)tooknow 更多關於常見的名稱和 hello 簽發者。 |
| ReverseProxyCertificate |建議針對測試環境。 這是選擇性的憑證，可以指定是否要讓 toosecure 您[反向 Proxy](service-fabric-reverseproxy.md)。 如果您使用此憑證，請務必在 nodeTypes 中設定 reverseProxyEndpointPort。 |
| ReverseProxyCertificateCommonNames |建議針對生產環境。 這是選擇性的憑證，可以指定是否要讓 toosecure 您[反向 Proxy](service-fabric-reverseproxy.md)。 如果您使用此憑證，請務必在 nodeTypes 中設定 reverseProxyEndpointPort。 |

以下是範例叢集組態即已提供 hello 叢集、 伺服器和用戶端憑證。 請注意，叢集 / server / reverseProxy 憑證、 憑證指紋和一般名稱不允許 toobe 設定一起 hello 和憑證類型。

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a>憑證變換
使用憑證通用名稱而非指紋時，憑證變換並不需要叢集設定升級。
如果憑證變換牽涉到簽發者會彙總，請保留 hello 舊的簽發者憑證 hello 憑證存放區中安裝新簽發者憑證 hello 之後至少 2 小時。

## <a name="acquire-hello-x509-certificates"></a>取得 hello X.509 憑證
toosecure hello 叢集內的通訊，您首先需要 tooobtain X.509 憑證的叢集節點。 此外，toolimit 連接 toothis 叢集 tooauthorized 機器/使用者，您將需要 tooobtain 並安裝憑證的 hello 用戶端電腦。

對於生產工作負載執行的叢集，您應該使用[憑證授權單位 (CA)](https://en.wikipedia.org/wiki/Certificate_authority)簽署 X.509 憑證 toosecure hello 叢集。 如需取得這些憑證的詳細資訊，請移至太[How to： 取得憑證](http://msdn.microsoft.com/library/aa702761.aspx)。

您用於測試用途的叢集，您可以選擇 toouse 自我簽署的憑證。

## <a name="optional-create-a-self-signed-certificate"></a>選擇性：建立自我簽署憑證
其中一種方式 toocreate 可以正確保護的自我簽署憑證為 toouse hello *CertSetup.ps1* hello 目錄中的 hello Service Fabric SDK 資料夾中的指令碼*C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*。 編輯 hello 憑證此檔案 toochange hello 預設名稱 (尋找 hello 值*CN = ServiceFabricDevClusterCert*)。 執行此指令碼為 `.\CertSetup.ps1 -Install`。

現在匯出 hello 憑證 tooa PFX 檔與受保護的密碼。 先取得 hello hello 憑證指紋。 從 hello*啟動*功能表上，執行 hello*管理的電腦憑證*。 瀏覽 toohello**本機電腦 \ 個人**資料夾，然後尋找 hello 憑證剛建立。 按兩下 hello 憑證 tooopen 它選取 hello*詳細資料* 索引標籤並捲動 toohello*指紋*欄位。 移除 hello 空白之後複製 hello PowerShell 命令下, 面 hello 指紋值。  變更 hello`String`值 tooa 適合的安全密碼 tooprotect 它，並執行下列 PowerShell 中的 hello:

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

toosee hello 詳細資料，hello 上安裝的憑證的電腦，您可以執行下列 PowerShell 命令的 hello:

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

或者，如果您有 Azure 訂用帳戶，請遵循 hello 區段[新增憑證 tooKey 保存庫](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault)。

## <a name="install-hello-certificates"></a>安裝 hello 憑證
一旦您擁有的憑證，您可以在 hello 叢集節點上安裝它們。 您的節點需要 toohave hello 最新的 Windows PowerShell 3.x 上加以安裝。 您將需要 toorepeat 上每個節點，這些步驟，叢集和伺服器憑證，以及任何次要憑證。

1. 複製 hello.pfx 檔案 toohello 節點。
2. 開啟 PowerShell 視窗，以系統管理員，並輸入下列命令的 hello。 取代 hello *$pswd*與 hello 您用 toocreate 此憑證的密碼。 取代 hello *$PfxFilePath* hello.pfx 複製的 toothis 節點 hello 完整路徑。
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. 現在設定 hello 此憑證上的存取控制，讓 hello Service Fabric 處理序，以便在 hello Network Service 帳戶下執行時，可以執行下列指令碼的 hello 來使用它。 提供 hello 憑證和 hello 服務帳戶的 「 網路服務 」 的 hello 指紋。 您可以檢查該 hello Acl hello 憑證上的開啟中的 hello 憑證是否正確*啟動* > *管理的電腦憑證*並查看*的所有工作* > *管理私用金鑰*。
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. 每個伺服器憑證重複上述步驟，hello。 您也可以使用這些步驟 tooinstall hello 用戶端憑證 hello 機器上的 tooallow 存取 toohello 叢集。

## <a name="create-hello-secure-cluster"></a>建立 hello 安全叢集
設定 hello 之後**安全性**區段 hello **ClusterConfig.X509.MultiMachine.json**檔案中，您可以繼續太[建立您的叢集](service-fabric-cluster-creation-for-windows-server.md#createcluster)區段 tooconfigurehello 節點，並建立 hello 獨立叢集。 請記住 toouse hello **ClusterConfig.X509.MultiMachine.json**建立 hello 叢集時的檔案。 例如，您的命令看起來可能 hello 如下：

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

一旦您擁有 hello 安全獨立 Windows 叢集已順利執行，並讓安裝程式 hello 已驗證的用戶端 tooconnect tooit，請遵循 hello > 一節[連接 tooa 安全叢集使用 PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit。 例如：

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

然後，您可以執行其他的 PowerShell 命令 toowork 與此叢集。 例如， [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow 上此安全叢集的節點清單。


tooremove hello 叢集中，您用來下載 hello Service Fabric 封裝 hello 叢集上的 toohello 節點連接、 開啟命令列並瀏覽 toohello 套件資料夾。 現在，執行下列命令的 hello:

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> 憑證不正確組態可能會阻止 hello 叢集接下來，在部署期間。 tooself-診斷安全性問題，請查看事件檢視器群組*Applications and Services Logs* > *Microsoft Service Fabric*。
> 
> 

