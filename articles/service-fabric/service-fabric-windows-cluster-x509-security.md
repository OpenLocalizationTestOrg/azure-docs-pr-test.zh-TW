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
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="c0c25-103">使用 X.509 憑證保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="c0c25-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="c0c25-104">本文說明如何 toosecure hello 溝通 hello 獨立 Windows 叢集的不同節點，以及如何 tooauthenticate 連接的用戶端 toothis 叢集會使用 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="c0c25-104">This article describes how toosecure hello communication between hello various nodes of your standalone Windows cluster, as well as how tooauthenticate clients connecting toothis cluster, using X.509 certificates.</span></span> <span data-ttu-id="c0c25-105">這樣可以確保，只有授權的使用者可以存取 hello 叢集 hello 部署之應用程式執行管理工作。</span><span class="sxs-lookup"><span data-stu-id="c0c25-105">This ensures that only authorized users can access hello cluster, hello deployed applications and perform management tasks.</span></span>  <span data-ttu-id="c0c25-106">建立 hello 叢集時，應該 hello 叢集上啟用憑證安全性。</span><span class="sxs-lookup"><span data-stu-id="c0c25-106">Certificate security should be enabled on hello cluster when hello cluster is created.</span></span>  

<span data-ttu-id="c0c25-107">如需諸如節點對節點安全性、用戶端對節點安全性、角色型存取控制等有關叢集安全性的詳細資訊，請參閱 [叢集安全性案例](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="c0c25-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="c0c25-108">您需要哪些憑證？</span><span class="sxs-lookup"><span data-stu-id="c0c25-108">Which certificates will you need?</span></span>
<span data-ttu-id="c0c25-109">toostart，[下載 hello 獨立叢集封裝](service-fabric-cluster-creation-for-windows-server.md#downloadpackage)tooone 的 hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="c0c25-109">toostart with, [download hello standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone of hello nodes in your cluster.</span></span> <span data-ttu-id="c0c25-110">在 hello 下載封裝，您會發現**ClusterConfig.X509.MultiMachine.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="c0c25-110">In hello downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="c0c25-111">開啟 hello 檔案，並檢閱 hello 區段**安全性**下 hello**屬性**> 一節：</span><span class="sxs-lookup"><span data-stu-id="c0c25-111">Open hello file and review hello section for **security** under hello **properties** section:</span></span>

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

<span data-ttu-id="c0c25-112">本章節描述您需要為保護您的獨立 Windows 叢集的 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="c0c25-112">This section describes hello certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="c0c25-113">如果您指定叢集憑證時，設定 hello 值**ClusterCredentialType** too_**X509**_。如果您指定的外部連接的伺服器憑證時，設定 hello **ServerCredentialType**太_**X509**_。雖然並非必要，但建議 toohave 正確安全叢集的兩個這些憑證。如果這些值設定得*X509*接著，您也必須指定 hello 對應憑證或服務的網狀架構將會擲回例外狀況。在某些情況下，您可能只想 toospecify hello _ClientCertificateThumbprints_或_ReverseProxyCertificate_。在這些情況下，您需要設定_ClusterCredentialType_或_ServerCredentialType_ too_X509_。</span><span class="sxs-lookup"><span data-stu-id="c0c25-113">If you are specifying a cluster certificate, set hello value of **ClusterCredentialType** too_**X509**_. If you are specifying server certificate for outside connections, set hello **ServerCredentialType** too_**X509**_. Although not mandatory, we recommend toohave both these certificates for a properly secured cluster. If you set these values too*X509* then you must also specify hello corresponding certificates or Service Fabric will throw an exception. In some scenarios, you may only want toospecify hello _ClientCertificateThumbprints_ or _ReverseProxyCertificate_. In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ too_X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="c0c25-114">A[指紋](https://en.wikipedia.org/wiki/Public_key_fingerprint)是 hello 主要身分識別的憑證。</span><span class="sxs-lookup"><span data-stu-id="c0c25-114">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is hello primary identity of a certificate.</span></span> <span data-ttu-id="c0c25-115">讀取[如何 tooretrieve 憑證的指紋](https://msdn.microsoft.com/library/ms734695.aspx)toofind 出 hello hello 您所建立的憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="c0c25-115">Read [How tooretrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) toofind out hello thumbprint of hello certificates that you create.</span></span>
> 
> 

<span data-ttu-id="c0c25-116">hello 下表列出您必須在叢集設定的 hello 憑證：</span><span class="sxs-lookup"><span data-stu-id="c0c25-116">hello following table lists hello certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="c0c25-117">**CertificateInformation 設定**</span><span class="sxs-lookup"><span data-stu-id="c0c25-117">**CertificateInformation Setting**</span></span> | <span data-ttu-id="c0c25-118">**說明**</span><span class="sxs-lookup"><span data-stu-id="c0c25-118">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c0c25-119">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="c0c25-119">ClusterCertificate</span></span> |<span data-ttu-id="c0c25-120">建議針對測試環境。</span><span class="sxs-lookup"><span data-stu-id="c0c25-120">Recommended for test environment.</span></span> <span data-ttu-id="c0c25-121">此憑證是在叢集上的 hello 節點之間需要的 toosecure hello 通訊。</span><span class="sxs-lookup"><span data-stu-id="c0c25-121">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="c0c25-122">您可以使用兩個不同的憑證 (主要和次要) 進行更新。</span><span class="sxs-lookup"><span data-stu-id="c0c25-122">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="c0c25-123">設定在 hello hello hello 主要憑證指紋**指紋**> 一節，在 hello 次要 hello **ThumbprintSecondary**變數。</span><span class="sxs-lookup"><span data-stu-id="c0c25-123">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="c0c25-124">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="c0c25-124">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="c0c25-125">建議針對生產環境。</span><span class="sxs-lookup"><span data-stu-id="c0c25-125">Recommended for production environment.</span></span> <span data-ttu-id="c0c25-126">此憑證是在叢集上的 hello 節點之間需要的 toosecure hello 通訊。</span><span class="sxs-lookup"><span data-stu-id="c0c25-126">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="c0c25-127">您可以使用一或兩個叢集憑證通用名稱。</span><span class="sxs-lookup"><span data-stu-id="c0c25-127">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="c0c25-128">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="c0c25-128">ServerCertificate</span></span> |<span data-ttu-id="c0c25-129">建議針對測試環境。</span><span class="sxs-lookup"><span data-stu-id="c0c25-129">Recommended for test environment.</span></span> <span data-ttu-id="c0c25-130">當它嘗試 tooconnect toothis 叢集時，此憑證會呈現 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c0c25-130">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="c0c25-131">為了方便起見，您可以選擇 toouse 相同憑證的 hello *ClusterCertificate*和*ServerCertificate*。</span><span class="sxs-lookup"><span data-stu-id="c0c25-131">For convenience, you can choose toouse hello same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="c0c25-132">您可以使用兩個不同的伺服器憑證 (主要和次要) 進行更新。</span><span class="sxs-lookup"><span data-stu-id="c0c25-132">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="c0c25-133">設定在 hello hello hello 主要憑證指紋**指紋**> 一節，在 hello 次要 hello **ThumbprintSecondary**變數。</span><span class="sxs-lookup"><span data-stu-id="c0c25-133">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="c0c25-134">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="c0c25-134">ServerCertificateCommonNames</span></span> |<span data-ttu-id="c0c25-135">建議針對生產環境。</span><span class="sxs-lookup"><span data-stu-id="c0c25-135">Recommended for production environment.</span></span> <span data-ttu-id="c0c25-136">當它嘗試 tooconnect toothis 叢集時，此憑證會呈現 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c0c25-136">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="c0c25-137">為了方便起見，您可以選擇 toouse 相同憑證的 hello *ClusterCertificateCommonNames*和*ServerCertificateCommonNames*。</span><span class="sxs-lookup"><span data-stu-id="c0c25-137">For convenience, you can choose toouse hello same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="c0c25-138">您可以使用一或兩個伺服器憑證通用名稱。</span><span class="sxs-lookup"><span data-stu-id="c0c25-138">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="c0c25-139">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="c0c25-139">ClientCertificateThumbprints</span></span> |<span data-ttu-id="c0c25-140">這是一組您想 tooinstall hello 驗證用戶端上的憑證。</span><span class="sxs-lookup"><span data-stu-id="c0c25-140">This is a set of certificates that you want tooinstall on hello authenticated clients.</span></span> <span data-ttu-id="c0c25-141">您可以有數個不同的用戶端憑證安裝在您想 tooallow 存取 toohello 叢集 hello 機器上。</span><span class="sxs-lookup"><span data-stu-id="c0c25-141">You can have a number of different client certificates installed on hello machines that you want tooallow access toohello cluster.</span></span> <span data-ttu-id="c0c25-142">在 hello 中設定每個憑證的指紋，hello **CertificateThumbprint**變數。</span><span class="sxs-lookup"><span data-stu-id="c0c25-142">Set hello thumbprint of each certificate in hello **CertificateThumbprint** variable.</span></span> <span data-ttu-id="c0c25-143">如果您設定 hello **IsAdmin**太*true*，然後 hello 與在其上安裝此憑證的用戶端可以執行系統管理員在 hello 叢集上的管理活動。</span><span class="sxs-lookup"><span data-stu-id="c0c25-143">If you set hello **IsAdmin** too*true*, then hello client with this certificate installed on it can do administrator management activities on hello cluster.</span></span> <span data-ttu-id="c0c25-144">如果 hello **IsAdmin**是*false*，hello 與此憑證的用戶端只能執行 hello 動作允許使用者存取權限，通常是唯讀的。</span><span class="sxs-lookup"><span data-stu-id="c0c25-144">If hello **IsAdmin** is *false*, hello client with this certificate can only perform hello actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="c0c25-145">如需角色的詳細資訊，請參閱 [角色型存取控制 (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="c0c25-145">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="c0c25-146">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="c0c25-146">ClientCertificateCommonNames</span></span> |<span data-ttu-id="c0c25-147">設定 hello 的一般名稱的第一個用戶端憑證 hello hello **CertificateCommonName**。</span><span class="sxs-lookup"><span data-stu-id="c0c25-147">Set hello common name of hello first client certificate for hello **CertificateCommonName**.</span></span> <span data-ttu-id="c0c25-148">hello **CertificateIssuerThumbprint** hello 指紋為 hello 這個憑證的簽發者。</span><span class="sxs-lookup"><span data-stu-id="c0c25-148">hello **CertificateIssuerThumbprint** is hello thumbprint for hello issuer of this certificate.</span></span> <span data-ttu-id="c0c25-149">讀取[使用憑證](https://msdn.microsoft.com/library/ms731899.aspx)tooknow 更多關於常見的名稱和 hello 簽發者。</span><span class="sxs-lookup"><span data-stu-id="c0c25-149">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) tooknow more about common names and hello issuer.</span></span> |
| <span data-ttu-id="c0c25-150">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="c0c25-150">ReverseProxyCertificate</span></span> |<span data-ttu-id="c0c25-151">建議針對測試環境。</span><span class="sxs-lookup"><span data-stu-id="c0c25-151">Recommended for test environment.</span></span> <span data-ttu-id="c0c25-152">這是選擇性的憑證，可以指定是否要讓 toosecure 您[反向 Proxy](service-fabric-reverseproxy.md)。</span><span class="sxs-lookup"><span data-stu-id="c0c25-152">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="c0c25-153">如果您使用此憑證，請務必在 nodeTypes 中設定 reverseProxyEndpointPort。</span><span class="sxs-lookup"><span data-stu-id="c0c25-153">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="c0c25-154">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="c0c25-154">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="c0c25-155">建議針對生產環境。</span><span class="sxs-lookup"><span data-stu-id="c0c25-155">Recommended for production environment.</span></span> <span data-ttu-id="c0c25-156">這是選擇性的憑證，可以指定是否要讓 toosecure 您[反向 Proxy](service-fabric-reverseproxy.md)。</span><span class="sxs-lookup"><span data-stu-id="c0c25-156">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="c0c25-157">如果您使用此憑證，請務必在 nodeTypes 中設定 reverseProxyEndpointPort。</span><span class="sxs-lookup"><span data-stu-id="c0c25-157">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="c0c25-158">以下是範例叢集組態即已提供 hello 叢集、 伺服器和用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c0c25-158">Here is example cluster configuration where hello Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="c0c25-159">請注意，叢集 / server / reverseProxy 憑證、 憑證指紋和一般名稱不允許 toobe 設定一起 hello 和憑證類型。</span><span class="sxs-lookup"><span data-stu-id="c0c25-159">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed toobe configured together for hello same cert type.</span></span>

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

## <a name="certificate-roll-over"></a><span data-ttu-id="c0c25-160">憑證變換</span><span class="sxs-lookup"><span data-stu-id="c0c25-160">Certificate roll over</span></span>
<span data-ttu-id="c0c25-161">使用憑證通用名稱而非指紋時，憑證變換並不需要叢集設定升級。</span><span class="sxs-lookup"><span data-stu-id="c0c25-161">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="c0c25-162">如果憑證變換牽涉到簽發者會彙總，請保留 hello 舊的簽發者憑證 hello 憑證存放區中安裝新簽發者憑證 hello 之後至少 2 小時。</span><span class="sxs-lookup"><span data-stu-id="c0c25-162">If certificate roll over involves issuer roll over, please keep hello old issuer cert in hello cert store at least 2 hours after installing hello new issuer cert.</span></span>

## <a name="acquire-hello-x509-certificates"></a><span data-ttu-id="c0c25-163">取得 hello X.509 憑證</span><span class="sxs-lookup"><span data-stu-id="c0c25-163">Acquire hello X.509 certificates</span></span>
<span data-ttu-id="c0c25-164">toosecure hello 叢集內的通訊，您首先需要 tooobtain X.509 憑證的叢集節點。</span><span class="sxs-lookup"><span data-stu-id="c0c25-164">toosecure communication within hello cluster, you will first need tooobtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="c0c25-165">此外，toolimit 連接 toothis 叢集 tooauthorized 機器/使用者，您將需要 tooobtain 並安裝憑證的 hello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="c0c25-165">Additionally, toolimit connection toothis cluster tooauthorized machines/users, you will need tooobtain and install certificates for hello client machines.</span></span>

<span data-ttu-id="c0c25-166">對於生產工作負載執行的叢集，您應該使用[憑證授權單位 (CA)](https://en.wikipedia.org/wiki/Certificate_authority)簽署 X.509 憑證 toosecure hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="c0c25-166">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate toosecure hello cluster.</span></span> <span data-ttu-id="c0c25-167">如需取得這些憑證的詳細資訊，請移至太[How to： 取得憑證](http://msdn.microsoft.com/library/aa702761.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c0c25-167">For details on obtaining these certificates, go too[How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="c0c25-168">您用於測試用途的叢集，您可以選擇 toouse 自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="c0c25-168">For clusters that you use for test purposes, you can choose toouse a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="c0c25-169">選擇性：建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="c0c25-169">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="c0c25-170">其中一種方式 toocreate 可以正確保護的自我簽署憑證為 toouse hello *CertSetup.ps1* hello 目錄中的 hello Service Fabric SDK 資料夾中的指令碼*C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*。</span><span class="sxs-lookup"><span data-stu-id="c0c25-170">One way toocreate a self-signed cert that can be secured correctly is toouse hello *CertSetup.ps1* script in hello Service Fabric SDK folder in hello directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="c0c25-171">編輯 hello 憑證此檔案 toochange hello 預設名稱 (尋找 hello 值*CN = ServiceFabricDevClusterCert*)。</span><span class="sxs-lookup"><span data-stu-id="c0c25-171">Edit this file toochange hello default name of hello certificate (look for hello value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="c0c25-172">執行此指令碼為 `.\CertSetup.ps1 -Install`。</span><span class="sxs-lookup"><span data-stu-id="c0c25-172">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="c0c25-173">現在匯出 hello 憑證 tooa PFX 檔與受保護的密碼。</span><span class="sxs-lookup"><span data-stu-id="c0c25-173">Now export hello certificate tooa PFX file with a protected password.</span></span> <span data-ttu-id="c0c25-174">先取得 hello hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="c0c25-174">First get hello thumbprint of hello certificate.</span></span> <span data-ttu-id="c0c25-175">從 hello*啟動*功能表上，執行 hello*管理的電腦憑證*。</span><span class="sxs-lookup"><span data-stu-id="c0c25-175">From hello *Start* menu, run hello *Manage computer certificates*.</span></span> <span data-ttu-id="c0c25-176">瀏覽 toohello**本機電腦 \ 個人**資料夾，然後尋找 hello 憑證剛建立。</span><span class="sxs-lookup"><span data-stu-id="c0c25-176">Navigate toohello **Local Computer\Personal** folder and find hello certificate you just created.</span></span> <span data-ttu-id="c0c25-177">按兩下 hello 憑證 tooopen 它選取 hello*詳細資料* 索引標籤並捲動 toohello*指紋*欄位。</span><span class="sxs-lookup"><span data-stu-id="c0c25-177">Double-click hello certificate tooopen it, select hello *Details* tab and scroll down toohello *Thumbprint* field.</span></span> <span data-ttu-id="c0c25-178">移除 hello 空白之後複製 hello PowerShell 命令下, 面 hello 指紋值。</span><span class="sxs-lookup"><span data-stu-id="c0c25-178">Copy hello thumbprint value into hello PowerShell command below, after removing hello spaces.</span></span>  <span data-ttu-id="c0c25-179">變更 hello`String`值 tooa 適合的安全密碼 tooprotect 它，並執行下列 PowerShell 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="c0c25-179">Change hello `String` value tooa suitable secure password tooprotect it and run hello following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="c0c25-180">toosee hello 詳細資料，hello 上安裝的憑證的電腦，您可以執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="c0c25-180">toosee hello details of a certificate installed on hello machine you can run hello following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="c0c25-181">或者，如果您有 Azure 訂用帳戶，請遵循 hello 區段[新增憑證 tooKey 保存庫](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault)。</span><span class="sxs-lookup"><span data-stu-id="c0c25-181">Alternatively, if you have an Azure subscription, follow hello section [Add certificates tooKey Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-hello-certificates"></a><span data-ttu-id="c0c25-182">安裝 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="c0c25-182">Install hello certificates</span></span>
<span data-ttu-id="c0c25-183">一旦您擁有的憑證，您可以在 hello 叢集節點上安裝它們。</span><span class="sxs-lookup"><span data-stu-id="c0c25-183">Once you have certificate(s), you can install them on hello cluster nodes.</span></span> <span data-ttu-id="c0c25-184">您的節點需要 toohave hello 最新的 Windows PowerShell 3.x 上加以安裝。</span><span class="sxs-lookup"><span data-stu-id="c0c25-184">Your nodes need toohave hello latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="c0c25-185">您將需要 toorepeat 上每個節點，這些步驟，叢集和伺服器憑證，以及任何次要憑證。</span><span class="sxs-lookup"><span data-stu-id="c0c25-185">You will need toorepeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="c0c25-186">複製 hello.pfx 檔案 toohello 節點。</span><span class="sxs-lookup"><span data-stu-id="c0c25-186">Copy hello .pfx file(s) toohello node.</span></span>
2. <span data-ttu-id="c0c25-187">開啟 PowerShell 視窗，以系統管理員，並輸入下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="c0c25-187">Open a PowerShell window as an administrator and enter hello following commands.</span></span> <span data-ttu-id="c0c25-188">取代 hello *$pswd*與 hello 您用 toocreate 此憑證的密碼。</span><span class="sxs-lookup"><span data-stu-id="c0c25-188">Replace hello *$pswd* with hello password that you used toocreate this certificate.</span></span> <span data-ttu-id="c0c25-189">取代 hello *$PfxFilePath* hello.pfx 複製的 toothis 節點 hello 完整路徑。</span><span class="sxs-lookup"><span data-stu-id="c0c25-189">Replace hello *$PfxFilePath* with hello full path of hello .pfx copied toothis node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="c0c25-190">現在設定 hello 此憑證上的存取控制，讓 hello Service Fabric 處理序，以便在 hello Network Service 帳戶下執行時，可以執行下列指令碼的 hello 來使用它。</span><span class="sxs-lookup"><span data-stu-id="c0c25-190">Now set hello access control on this certificate so that hello Service Fabric process, which runs under hello Network Service account, can use it by running hello following script.</span></span> <span data-ttu-id="c0c25-191">提供 hello 憑證和 hello 服務帳戶的 「 網路服務 」 的 hello 指紋。</span><span class="sxs-lookup"><span data-stu-id="c0c25-191">Provide hello thumbprint of hello certificate and "NETWORK SERVICE" for hello service account.</span></span> <span data-ttu-id="c0c25-192">您可以檢查該 hello Acl hello 憑證上的開啟中的 hello 憑證是否正確*啟動* > *管理的電腦憑證*並查看*的所有工作* > *管理私用金鑰*。</span><span class="sxs-lookup"><span data-stu-id="c0c25-192">You can check that hello ACLs on hello certificate are correct by opening hello certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
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
4. <span data-ttu-id="c0c25-193">每個伺服器憑證重複上述步驟，hello。</span><span class="sxs-lookup"><span data-stu-id="c0c25-193">Repeat hello steps above for each server certificate.</span></span> <span data-ttu-id="c0c25-194">您也可以使用這些步驟 tooinstall hello 用戶端憑證 hello 機器上的 tooallow 存取 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="c0c25-194">You can also use these steps tooinstall hello client certificates on hello machines that you want tooallow access toohello cluster.</span></span>

## <a name="create-hello-secure-cluster"></a><span data-ttu-id="c0c25-195">建立 hello 安全叢集</span><span class="sxs-lookup"><span data-stu-id="c0c25-195">Create hello secure cluster</span></span>
<span data-ttu-id="c0c25-196">設定 hello 之後**安全性**區段 hello **ClusterConfig.X509.MultiMachine.json**檔案中，您可以繼續太[建立您的叢集](service-fabric-cluster-creation-for-windows-server.md#createcluster)區段 tooconfigurehello 節點，並建立 hello 獨立叢集。</span><span class="sxs-lookup"><span data-stu-id="c0c25-196">After configuring hello **security** section of hello **ClusterConfig.X509.MultiMachine.json** file, you can proceed too[Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section tooconfigure hello nodes and create hello standalone cluster.</span></span> <span data-ttu-id="c0c25-197">請記住 toouse hello **ClusterConfig.X509.MultiMachine.json**建立 hello 叢集時的檔案。</span><span class="sxs-lookup"><span data-stu-id="c0c25-197">Remember toouse hello **ClusterConfig.X509.MultiMachine.json** file while creating hello cluster.</span></span> <span data-ttu-id="c0c25-198">例如，您的命令看起來可能 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="c0c25-198">For example, your command might look like hello following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="c0c25-199">一旦您擁有 hello 安全獨立 Windows 叢集已順利執行，並讓安裝程式 hello 已驗證的用戶端 tooconnect tooit，請遵循 hello > 一節[連接 tooa 安全叢集使用 PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit。</span><span class="sxs-lookup"><span data-stu-id="c0c25-199">Once you have hello secure standalone Windows cluster successfully running, and have setup hello authenticated clients tooconnect tooit, follow hello section [Connect tooa secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span></span> <span data-ttu-id="c0c25-200">例如：</span><span class="sxs-lookup"><span data-stu-id="c0c25-200">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="c0c25-201">然後，您可以執行其他的 PowerShell 命令 toowork 與此叢集。</span><span class="sxs-lookup"><span data-stu-id="c0c25-201">You can then run other PowerShell commands toowork with this cluster.</span></span> <span data-ttu-id="c0c25-202">例如， [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow 上此安全叢集的節點清單。</span><span class="sxs-lookup"><span data-stu-id="c0c25-202">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="c0c25-203">tooremove hello 叢集中，您用來下載 hello Service Fabric 封裝 hello 叢集上的 toohello 節點連接、 開啟命令列並瀏覽 toohello 套件資料夾。</span><span class="sxs-lookup"><span data-stu-id="c0c25-203">tooremove hello cluster, connect toohello node on hello cluster where you downloaded hello Service Fabric package, open a command line and navigate toohello package folder.</span></span> <span data-ttu-id="c0c25-204">現在，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="c0c25-204">Now run hello following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="c0c25-205">憑證不正確組態可能會阻止 hello 叢集接下來，在部署期間。</span><span class="sxs-lookup"><span data-stu-id="c0c25-205">Incorrect certificate configuration may prevent hello cluster from coming up during deployment.</span></span> <span data-ttu-id="c0c25-206">tooself-診斷安全性問題，請查看事件檢視器群組*Applications and Services Logs* > *Microsoft Service Fabric*。</span><span class="sxs-lookup"><span data-stu-id="c0c25-206">tooself-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

