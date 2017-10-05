---
title: "使用憑證保護 Windows 上的 Azure Service Fabric 叢集 | Microsoft Docs"
description: "本文說明如何保護獨立或私人叢集內以及用戶端與叢集之間的通訊。"
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
ms.openlocfilehash: 71ece1e43cc3c4ac3350cd59633065de06672420
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="ac78e-103">使用 X.509 憑證保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="ac78e-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="ac78e-104">本文說明如何保護獨立 Windows 叢集的各個節點之間的通訊，以及如何使用 X.509 憑證來驗證連線到此叢集的用戶端。</span><span class="sxs-lookup"><span data-stu-id="ac78e-104">This article describes how to secure the communication between the various nodes of your standalone Windows cluster, as well as how to authenticate clients connecting to this cluster, using X.509 certificates.</span></span> <span data-ttu-id="ac78e-105">這可確保只有已獲授權的使用者可以存取叢集和已部署的應用程式，以及執行管理工作。</span><span class="sxs-lookup"><span data-stu-id="ac78e-105">This ensures that only authorized users can access the cluster, the deployed applications and perform management tasks.</span></span>  <span data-ttu-id="ac78e-106">憑證安全性應在叢集建立之時先在叢集上啟用。</span><span class="sxs-lookup"><span data-stu-id="ac78e-106">Certificate security should be enabled on the cluster when the cluster is created.</span></span>  

<span data-ttu-id="ac78e-107">如需諸如節點對節點安全性、用戶端對節點安全性、角色型存取控制等有關叢集安全性的詳細資訊，請參閱 [叢集安全性案例](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="ac78e-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="ac78e-108">您需要哪些憑證？</span><span class="sxs-lookup"><span data-stu-id="ac78e-108">Which certificates will you need?</span></span>
<span data-ttu-id="ac78e-109">一開始，請 [將獨立叢集封裝](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) 下載至叢集中的其中一個節點。</span><span class="sxs-lookup"><span data-stu-id="ac78e-109">To start with, [download the standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) to one of the nodes in your cluster.</span></span> <span data-ttu-id="ac78e-110">在下載的套件中，您會找到 **ClusterConfig.X509.MultiMachine.json** 檔案。</span><span class="sxs-lookup"><span data-stu-id="ac78e-110">In the downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="ac78e-111">開啟檔案，檢閱 **properties** 區段下的 **security** 區段：</span><span class="sxs-lookup"><span data-stu-id="ac78e-111">Open the file and review the section for **security** under the **properties** section:</span></span>

```JSON
"security": {
    "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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

<span data-ttu-id="ac78e-112">此區段描述保護獨立 Windows 叢集所需的憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-112">This section describes the certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="ac78e-113">如果您指定叢集憑證，請將**ClusterCredentialType** 的值設定為 _**X509**_。</span><span class="sxs-lookup"><span data-stu-id="ac78e-113">If you are specifying a cluster certificate, set the value of **ClusterCredentialType** to _**X509**_.</span></span> <span data-ttu-id="ac78e-114">如果您指定外部連接的伺服器憑證，請將 **ServerCredentialType** 設定為 _**X509**_。</span><span class="sxs-lookup"><span data-stu-id="ac78e-114">If you are specifying server certificate for outside connections, set the **ServerCredentialType** to _**X509**_.</span></span> <span data-ttu-id="ac78e-115">雖然並非必要，但我們建議具備這兩個憑證以適當保護叢集。</span><span class="sxs-lookup"><span data-stu-id="ac78e-115">Although not mandatory, we recommend to have both these certificates for a properly secured cluster.</span></span> <span data-ttu-id="ac78e-116">如果您將這些值設定為 X509，則您也必須指定對應憑證或 Service Fabric 將會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ac78e-116">If you set these values to *X509* then you must also specify the corresponding certificates or Service Fabric will throw an exception.</span></span> <span data-ttu-id="ac78e-117">在某些情況下，您可能只想要指定 _ClientCertificateThumbprints_ 或 _ReverseProxyCertificate_。</span><span class="sxs-lookup"><span data-stu-id="ac78e-117">In some scenarios, you may only want to specify the _ClientCertificateThumbprints_ or _ReverseProxyCertificate_.</span></span> <span data-ttu-id="ac78e-118">在這些情況下，您需要將 _ClusterCredentialType_ 或 _ServerCredentialType_設定為 _X509_。</span><span class="sxs-lookup"><span data-stu-id="ac78e-118">In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ to _X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="ac78e-119">[指紋](https://en.wikipedia.org/wiki/Public_key_fingerprint) 是憑證的主要身分識別。</span><span class="sxs-lookup"><span data-stu-id="ac78e-119">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is the primary identity of a certificate.</span></span> <span data-ttu-id="ac78e-120">閱讀 [如何擷取憑證的指紋](https://msdn.microsoft.com/library/ms734695.aspx) ，以找出您所建立的憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="ac78e-120">Read [How to retrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) to find out the thumbprint of the certificates that you create.</span></span>
> 
> 

<span data-ttu-id="ac78e-121">下表列出您在設定叢集時所需的憑證：</span><span class="sxs-lookup"><span data-stu-id="ac78e-121">The following table lists the certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="ac78e-122">**CertificateInformation 設定**</span><span class="sxs-lookup"><span data-stu-id="ac78e-122">**CertificateInformation Setting**</span></span> | <span data-ttu-id="ac78e-123">**說明**</span><span class="sxs-lookup"><span data-stu-id="ac78e-123">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="ac78e-124">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="ac78e-124">ClusterCertificate</span></span> |<span data-ttu-id="ac78e-125">建議針對測試環境。</span><span class="sxs-lookup"><span data-stu-id="ac78e-125">Recommended for test environment.</span></span> <span data-ttu-id="ac78e-126">需有此憑證，才能保護叢集上節點之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="ac78e-126">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="ac78e-127">您可以使用兩個不同的憑證 (主要和次要) 進行更新。</span><span class="sxs-lookup"><span data-stu-id="ac78e-127">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="ac78e-128">在 **Thumbprint** 區段中設定主要憑證的指紋，以及在 **ThumbprintSecondary** 變數中設定次要憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="ac78e-128">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="ac78e-129">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="ac78e-129">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="ac78e-130">建議針對生產環境。</span><span class="sxs-lookup"><span data-stu-id="ac78e-130">Recommended for production environment.</span></span> <span data-ttu-id="ac78e-131">需有此憑證，才能保護叢集上節點之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="ac78e-131">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="ac78e-132">您可以使用一或兩個叢集憑證通用名稱。</span><span class="sxs-lookup"><span data-stu-id="ac78e-132">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="ac78e-133">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="ac78e-133">ServerCertificate</span></span> |<span data-ttu-id="ac78e-134">建議針對測試環境。</span><span class="sxs-lookup"><span data-stu-id="ac78e-134">Recommended for test environment.</span></span> <span data-ttu-id="ac78e-135">用戶端嘗試連線到此叢集時，會向用戶端此憑證顯示此憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-135">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="ac78e-136">為了方便起見，您可以選擇對 *ClusterCertificate* 和 *ServerCertificate* 使用相同的憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-136">For convenience, you can choose to use the same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="ac78e-137">您可以使用兩個不同的伺服器憑證 (主要和次要) 進行更新。</span><span class="sxs-lookup"><span data-stu-id="ac78e-137">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="ac78e-138">在 **Thumbprint** 區段中設定主要憑證的指紋，以及在 **ThumbprintSecondary** 變數中設定次要憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="ac78e-138">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="ac78e-139">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="ac78e-139">ServerCertificateCommonNames</span></span> |<span data-ttu-id="ac78e-140">建議針對生產環境。</span><span class="sxs-lookup"><span data-stu-id="ac78e-140">Recommended for production environment.</span></span> <span data-ttu-id="ac78e-141">用戶端嘗試連線到此叢集時，會向用戶端此憑證顯示此憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-141">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="ac78e-142">為了方便起見，您可以選擇對 ClusterCertificateCommonNames 和 ServerCertificateCommonNames 使用相同的憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-142">For convenience, you can choose to use the same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="ac78e-143">您可以使用一或兩個伺服器憑證通用名稱。</span><span class="sxs-lookup"><span data-stu-id="ac78e-143">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="ac78e-144">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="ac78e-144">ClientCertificateThumbprints</span></span> |<span data-ttu-id="ac78e-145">這是您想在經過驗證的用戶端上安裝的一組憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-145">This is a set of certificates that you want to install on the authenticated clients.</span></span> <span data-ttu-id="ac78e-146">在您要允許存取叢集的電腦上，您可以安裝數個不同的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-146">You can have a number of different client certificates installed on the machines that you want to allow access to the cluster.</span></span> <span data-ttu-id="ac78e-147">在 **CertificateThumbprint** 變數中設定每個憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="ac78e-147">Set the thumbprint of each certificate in the **CertificateThumbprint** variable.</span></span> <span data-ttu-id="ac78e-148">如果您將 **IsAdmin** 設為 *true*，則已安裝此憑證的用戶端可以對叢集執行系統管理員管理活動。</span><span class="sxs-lookup"><span data-stu-id="ac78e-148">If you set the **IsAdmin** to *true*, then the client with this certificate installed on it can do administrator management activities on the cluster.</span></span> <span data-ttu-id="ac78e-149">如果 **IsAdmin** 是 *false*，有此憑證的用戶端只能執行其使用者存取權限允許的動作，通常是唯讀。</span><span class="sxs-lookup"><span data-stu-id="ac78e-149">If the **IsAdmin** is *false*, the client with this certificate can only perform the actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="ac78e-150">如需角色的詳細資訊，請參閱 [角色型存取控制 (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="ac78e-150">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="ac78e-151">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="ac78e-151">ClientCertificateCommonNames</span></span> |<span data-ttu-id="ac78e-152">針對 **CertificateCommonName**設定第一個用戶端憑證的一般名稱。</span><span class="sxs-lookup"><span data-stu-id="ac78e-152">Set the common name of the first client certificate for the **CertificateCommonName**.</span></span> <span data-ttu-id="ac78e-153">**CertificateIssuerThumbprint** 是此憑證的簽發者指紋。</span><span class="sxs-lookup"><span data-stu-id="ac78e-153">The **CertificateIssuerThumbprint** is the thumbprint for the issuer of this certificate.</span></span> <span data-ttu-id="ac78e-154">閱讀 [使用憑證](https://msdn.microsoft.com/library/ms731899.aspx) ，以深入了解一般名稱和簽發者。</span><span class="sxs-lookup"><span data-stu-id="ac78e-154">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) to know more about common names and the issuer.</span></span> |
| <span data-ttu-id="ac78e-155">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="ac78e-155">ReverseProxyCertificate</span></span> |<span data-ttu-id="ac78e-156">建議針對測試環境。</span><span class="sxs-lookup"><span data-stu-id="ac78e-156">Recommended for test environment.</span></span> <span data-ttu-id="ac78e-157">如果您想要保護[反向 Proxy](service-fabric-reverseproxy.md)，可以指定此選擇性憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-157">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="ac78e-158">如果您使用此憑證，請務必在 nodeTypes 中設定 reverseProxyEndpointPort。</span><span class="sxs-lookup"><span data-stu-id="ac78e-158">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="ac78e-159">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="ac78e-159">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="ac78e-160">建議針對生產環境。</span><span class="sxs-lookup"><span data-stu-id="ac78e-160">Recommended for production environment.</span></span> <span data-ttu-id="ac78e-161">如果您想要保護[反向 Proxy](service-fabric-reverseproxy.md)，可以指定此選擇性憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-161">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="ac78e-162">如果您使用此憑證，請務必在 nodeTypes 中設定 reverseProxyEndpointPort。</span><span class="sxs-lookup"><span data-stu-id="ac78e-162">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="ac78e-163">以下是範例叢集組態，其中已提供叢集、 伺服器和用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-163">Here is example cluster configuration where the Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="ac78e-164">請注意，不可與相同憑證類型的 cluster/ server/ reverseProxy 憑證、指紋和通用名稱一起設定。</span><span class="sxs-lookup"><span data-stu-id="ac78e-164">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed to be configured together for the same cert type.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace the localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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

## <a name="certificate-roll-over"></a><span data-ttu-id="ac78e-165">憑證變換</span><span class="sxs-lookup"><span data-stu-id="ac78e-165">Certificate roll over</span></span>
<span data-ttu-id="ac78e-166">使用憑證通用名稱而非指紋時，憑證變換並不需要叢集設定升級。</span><span class="sxs-lookup"><span data-stu-id="ac78e-166">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="ac78e-167">如果憑證變換涉及簽發者變換，請在安裝新的簽發者憑證之後，將舊的簽發者憑證保留在憑證存放區至少 2 小時。</span><span class="sxs-lookup"><span data-stu-id="ac78e-167">If certificate roll over involves issuer roll over, please keep the old issuer cert in the cert store at least 2 hours after installing the new issuer cert.</span></span>

## <a name="acquire-the-x509-certificates"></a><span data-ttu-id="ac78e-168">取得 X.509 憑證</span><span class="sxs-lookup"><span data-stu-id="ac78e-168">Acquire the X.509 certificates</span></span>
<span data-ttu-id="ac78e-169">若要保護叢集內的通訊，您必須先取得叢集節點的 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-169">To secure communication within the cluster, you will first need to obtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="ac78e-170">此外，若要將此叢集的連線限制於經過授權的電腦/使用者，您必須取得並安裝這些用戶端電腦的憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-170">Additionally, to limit connection to this cluster to authorized machines/users, you will need to obtain and install certificates for the client machines.</span></span>

<span data-ttu-id="ac78e-171">對於執行生產環境工作負載的叢集，您應該使用 [憑證授權單位 (CA)](https://en.wikipedia.org/wiki/Certificate_authority) 簽署的 X.509 憑證來保護叢集。</span><span class="sxs-lookup"><span data-stu-id="ac78e-171">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate to secure the cluster.</span></span> <span data-ttu-id="ac78e-172">如需有關如何取得這些憑證的詳細資訊，請移至 [做法：取得憑證](http://msdn.microsoft.com/library/aa702761.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ac78e-172">For details on obtaining these certificates, go to [How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="ac78e-173">若是用於測試的叢集，您可以選擇使用自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-173">For clusters that you use for test purposes, you can choose to use a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="ac78e-174">選擇性：建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="ac78e-174">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="ac78e-175">若要建立可以正確保護的自我簽署憑證，其中一個做法是使用 *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure* 目錄下 Service Fabric SDK 資料夾中的 *CertSetup.ps1* 指令碼。</span><span class="sxs-lookup"><span data-stu-id="ac78e-175">One way to create a self-signed cert that can be secured correctly is to use the *CertSetup.ps1* script in the Service Fabric SDK folder in the directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="ac78e-176">編輯此檔案來變更憑證的預設名稱 (尋找值 CN=ServiceFabricDevClusterCert)。</span><span class="sxs-lookup"><span data-stu-id="ac78e-176">Edit this file to change the default name of the certificate (look for the value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="ac78e-177">執行此指令碼為 `.\CertSetup.ps1 -Install`。</span><span class="sxs-lookup"><span data-stu-id="ac78e-177">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="ac78e-178">現在將憑證匯出至 PFX 檔並設定保護密碼。</span><span class="sxs-lookup"><span data-stu-id="ac78e-178">Now export the certificate to a PFX file with a protected password.</span></span> <span data-ttu-id="ac78e-179">首先取得憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="ac78e-179">First get the thumbprint of the certificate.</span></span> <span data-ttu-id="ac78e-180">從 [啟動] 功能表中，執行 [管理電腦憑證]。</span><span class="sxs-lookup"><span data-stu-id="ac78e-180">From the *Start* menu, run the *Manage computer certificates*.</span></span> <span data-ttu-id="ac78e-181">瀏覽至 [本機電腦\個人] 資料夾，找到您剛建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-181">Navigate to the **Local Computer\Personal** folder and find the certificate you just created.</span></span> <span data-ttu-id="ac78e-182">按兩下憑證以開啟它，選取 [詳細資料] 索引標籤，然後向下捲動至 [指紋] 欄位。</span><span class="sxs-lookup"><span data-stu-id="ac78e-182">Double-click the certificate to open it, select the *Details* tab and scroll down to the *Thumbprint* field.</span></span> <span data-ttu-id="ac78e-183">在移除空格之後，將憑證指紋值複製到以下的 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="ac78e-183">Copy the thumbprint value into the PowerShell command below, after removing the spaces.</span></span>  <span data-ttu-id="ac78e-184">將 `String` 的值變更為適當的安全密碼加以保護，然後在 PowerShell 執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="ac78e-184">Change the `String` value to a suitable secure password to protect it and run the following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="ac78e-185">若要檢視電腦上安裝之憑證的詳細資訊，可以執行下列 PowerShell 命令︰</span><span class="sxs-lookup"><span data-stu-id="ac78e-185">To see the details of a certificate installed on the machine you can run the following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="ac78e-186">或者，如果您有 Azure 訂用帳戶，請遵循[新增憑證至金鑰保存庫](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="ac78e-186">Alternatively, if you have an Azure subscription, follow the section [Add certificates to Key Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-the-certificates"></a><span data-ttu-id="ac78e-187">安裝憑證</span><span class="sxs-lookup"><span data-stu-id="ac78e-187">Install the certificates</span></span>
<span data-ttu-id="ac78e-188">有了憑證之後，可以將它們安裝在叢集節點上。</span><span class="sxs-lookup"><span data-stu-id="ac78e-188">Once you have certificate(s), you can install them on the cluster nodes.</span></span> <span data-ttu-id="ac78e-189">節點上須已安裝最新的 Windows PowerShell 3.x。</span><span class="sxs-lookup"><span data-stu-id="ac78e-189">Your nodes need to have the latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="ac78e-190">您必須針對叢集和伺服器憑證及任何次要憑證，在每個節點上重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="ac78e-190">You will need to repeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="ac78e-191">將 .pfx 檔案複製到節點。</span><span class="sxs-lookup"><span data-stu-id="ac78e-191">Copy the .pfx file(s) to the node.</span></span>
2. <span data-ttu-id="ac78e-192">以系統管理員身分開啟 PowerShell 視窗並輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="ac78e-192">Open a PowerShell window as an administrator and enter the following commands.</span></span> <span data-ttu-id="ac78e-193">以您用來建立此憑證的密碼取代 $pswd  。</span><span class="sxs-lookup"><span data-stu-id="ac78e-193">Replace the *$pswd* with the password that you used to create this certificate.</span></span> <span data-ttu-id="ac78e-194">以複製到這個節點之 .pfx 的完整路徑取代 $PfxFilePath  。</span><span class="sxs-lookup"><span data-stu-id="ac78e-194">Replace the *$PfxFilePath* with the full path of the .pfx copied to this node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="ac78e-195">現在您必須在此憑證上設定存取控制，讓在「網路服務」帳戶下執行的 Service Fabric 程序可以藉由執行下列指令碼來使用它。</span><span class="sxs-lookup"><span data-stu-id="ac78e-195">Now set the access control on this certificate so that the Service Fabric process, which runs under the Network Service account, can use it by running the following script.</span></span> <span data-ttu-id="ac78e-196">提供憑證的指紋和服務帳戶的「網路服務」。</span><span class="sxs-lookup"><span data-stu-id="ac78e-196">Provide the thumbprint of the certificate and "NETWORK SERVICE" for the service account.</span></span> <span data-ttu-id="ac78e-197">您可以檢查憑證上的 ACL 是否正確，方法是在 [啟動]  >  [管理電腦憑證] 開啟憑證，並查看 [所有工作]  >  [管理私密金鑰]。</span><span class="sxs-lookup"><span data-stu-id="ac78e-197">You can check that the ACLs on the certificate are correct by opening the certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
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
   
    # Specify the user, the permissions and the permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of the machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get the current acl of the private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add the new ace to the acl of the private key
    $acl.SetAccessRule($accessRule)
   
    # Write back the new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe the access rights currently assigned to this certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="ac78e-198">為每個伺服器憑證重複上述步驟。</span><span class="sxs-lookup"><span data-stu-id="ac78e-198">Repeat the steps above for each server certificate.</span></span> <span data-ttu-id="ac78e-199">您也可以使用上述步在您要允許存取叢集的電腦上安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="ac78e-199">You can also use these steps to install the client certificates on the machines that you want to allow access to the cluster.</span></span>

## <a name="create-the-secure-cluster"></a><span data-ttu-id="ac78e-200">建立安全的叢集</span><span class="sxs-lookup"><span data-stu-id="ac78e-200">Create the secure cluster</span></span>
<span data-ttu-id="ac78e-201">設定 **ClusterConfig.X509.MultiMachine.json** 檔案的 **security** 區段後，您可以繼續進行[建立叢集](service-fabric-cluster-creation-for-windows-server.md#createcluster)一節，以設定節點和建立獨立叢集。</span><span class="sxs-lookup"><span data-stu-id="ac78e-201">After configuring the **security** section of the **ClusterConfig.X509.MultiMachine.json** file, you can proceed to [Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section to configure the nodes and create the standalone cluster.</span></span> <span data-ttu-id="ac78e-202">請記得在建立叢集時使用 **ClusterConfig.X509.MultiMachine.json** 檔案。</span><span class="sxs-lookup"><span data-stu-id="ac78e-202">Remember to use the **ClusterConfig.X509.MultiMachine.json** file while creating the cluster.</span></span> <span data-ttu-id="ac78e-203">例如，您的命令可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="ac78e-203">For example, your command might look like the following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="ac78e-204">順利執行安全的獨立 Windows 叢集，並已設定經過驗證的用戶端以進行連接之後，請依照[使用 PowerShell 來連線到安全的叢集](service-fabric-connect-to-secure-cluster.md#connectsecurecluster)一節來連接它。</span><span class="sxs-lookup"><span data-stu-id="ac78e-204">Once you have the secure standalone Windows cluster successfully running, and have setup the authenticated clients to connect to it, follow the section [Connect to a secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) to connect to it.</span></span> <span data-ttu-id="ac78e-205">例如：</span><span class="sxs-lookup"><span data-stu-id="ac78e-205">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="ac78e-206">然後，您可以執行其他的 PowerShell 命令以使用此叢集。</span><span class="sxs-lookup"><span data-stu-id="ac78e-206">You can then run other PowerShell commands to work with this cluster.</span></span> <span data-ttu-id="ac78e-207">例如，[Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) 可以顯示此安全叢集上的節點清單。</span><span class="sxs-lookup"><span data-stu-id="ac78e-207">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) to show a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="ac78e-208">若要移除叢集，連線至您下載 Service Fabric 套件的叢集節點，開啟命令列並導覽至套件資料夾。</span><span class="sxs-lookup"><span data-stu-id="ac78e-208">To remove the cluster, connect to the node on the cluster where you downloaded the Service Fabric package, open a command line and navigate to the package folder.</span></span> <span data-ttu-id="ac78e-209">現在執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="ac78e-209">Now run the following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="ac78e-210">不正確的憑證設定可能會在接下來的部署期間阻止叢集。</span><span class="sxs-lookup"><span data-stu-id="ac78e-210">Incorrect certificate configuration may prevent the cluster from coming up during deployment.</span></span> <span data-ttu-id="ac78e-211">若要自我診斷安全性問題，請查看事件檢視器群組 [應用程式及服務記錄檔]  >  [Microsoft Service Fabric]。</span><span class="sxs-lookup"><span data-stu-id="ac78e-211">To self-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

