---
title: "Service Fabric 容器安全性 aaaAzure |Microsoft 文件"
description: "了解現在 toosecure 容器服務。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a><span data-ttu-id="edd7c-103">容器安全性</span><span class="sxs-lookup"><span data-stu-id="edd7c-103">Container security</span></span>

<span data-ttu-id="edd7c-104">Service Fabric 提供服務內部容器 tooaccess 機制 hello （5.7 或更高版本） 的 Windows 或 Linux 叢集節點已安裝的憑證。</span><span class="sxs-lookup"><span data-stu-id="edd7c-104">Service Fabric provides a mechanism for services inside a container tooaccess a certificate that is installed on hello nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="edd7c-105">此外，Service Fabric 也會為 Windows 容器支援 gMSA (群組受管理的服務帳戶)。</span><span class="sxs-lookup"><span data-stu-id="edd7c-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="edd7c-106">容器的憑證管理</span><span class="sxs-lookup"><span data-stu-id="edd7c-106">Certificate management for containers</span></span>

<span data-ttu-id="edd7c-107">您可以藉由指定憑證來保護您的容器服務。</span><span class="sxs-lookup"><span data-stu-id="edd7c-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="edd7c-108">hello 憑證必須安裝在 hello hello 叢集節點上。</span><span class="sxs-lookup"><span data-stu-id="edd7c-108">hello certificate must be installed on hello nodes of hello cluster.</span></span> <span data-ttu-id="edd7c-109">hello 憑證中會提供資訊 hello 應用程式資訊清單下 hello`ContainerHostPolicies`標記為下列程式碼片段說明 hello:</span><span class="sxs-lookup"><span data-stu-id="edd7c-109">hello certificate information is provided in hello application manifest under hello `ContainerHostPolicies` tag as hello following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="edd7c-110">當啟動 hello 應用程式時，hello 執行階段讀取 hello 憑證，並產生 PFX 檔案和每個憑證的密碼。</span><span class="sxs-lookup"><span data-stu-id="edd7c-110">When starting hello application, hello runtime reads hello certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="edd7c-111">此 PFX 檔案和密碼是使用下列環境變數的 hello hello 容器內存取：</span><span class="sxs-lookup"><span data-stu-id="edd7c-111">This PFX file and password are accessible inside hello container using hello following environment variables:</span></span> 

* <span data-ttu-id="edd7c-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span><span class="sxs-lookup"><span data-stu-id="edd7c-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="edd7c-113">**Certificate_[CodePackageName]_[CertName]_Password**</span><span class="sxs-lookup"><span data-stu-id="edd7c-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="edd7c-114">hello 容器服務或處理序負責 hello PFX 檔案匯入到 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="edd7c-114">hello container service or process is responsible for importing hello PFX file into hello container.</span></span> <span data-ttu-id="edd7c-115">tooimport hello 憑證，您可以使用`setupentrypoint.sh`執行 hello 容器程序內的自訂程式碼或指令碼。</span><span class="sxs-lookup"><span data-stu-id="edd7c-115">tooimport hello certificate, you can use `setupentrypoint.sh` scripts or executed custom code within hello container process.</span></span> <span data-ttu-id="edd7c-116">在 C# 中的 hello PFX 檔案匯入的範例程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="edd7c-116">Sample code in C# for importing hello PFX file follows:</span></span>

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
<span data-ttu-id="edd7c-117">此 PFX 憑證可以用於驗證 hello 應用程式或服務或與其他服務的安全 commmunication。</span><span class="sxs-lookup"><span data-stu-id="edd7c-117">This PFX certificate can be used for authenticate hello application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="edd7c-118">為 Windows 容器設定 gMSA</span><span class="sxs-lookup"><span data-stu-id="edd7c-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="edd7c-119">tooset 向上 gMSA （群組受管理的服務帳戶），認證規格檔案 (`credspec`) 會放在 hello 叢集中所有節點。</span><span class="sxs-lookup"><span data-stu-id="edd7c-119">tooset up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in hello cluster.</span></span> <span data-ttu-id="edd7c-120">hello 檔案可以複製使用的 VM 延伸模組的所有節點上。</span><span class="sxs-lookup"><span data-stu-id="edd7c-120">hello file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="edd7c-121">hello`credspec`檔案必須包含 hello gMSA 帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="edd7c-121">hello `credspec` file must contain hello gMSA account information.</span></span> <span data-ttu-id="edd7c-122">如需有關 hello`credspec`檔案，請參閱[服務帳戶](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts)。</span><span class="sxs-lookup"><span data-stu-id="edd7c-122">For more information on hello `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="edd7c-123">hello 認證規格和 hello `Hostname` hello 應用程式資訊清單中所指定標記。</span><span class="sxs-lookup"><span data-stu-id="edd7c-123">hello credential specification and hello `Hostname` tag are specified in hello application manifest.</span></span> <span data-ttu-id="edd7c-124">hello`Hostname`標記必須符合 hello 容器下的執行的 hello gMSA 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="edd7c-124">hello `Hostname` tag must match hello gMSA account name that hello container runs under.</span></span>  <span data-ttu-id="edd7c-125">hello`Hostname`標記可讓本身 hello 容器 tooauthenticate tooother hello 使用 Kerberos 驗證的網域中的服務。</span><span class="sxs-lookup"><span data-stu-id="edd7c-125">hello `Hostname` tag allows hello container tooauthenticate itself tooother services in hello domain using Kerberos authentication.</span></span>  <span data-ttu-id="edd7c-126">指定 hello 範例`Hostname`和 hello `credspec` hello 在應用程式資訊清單會顯示在下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="edd7c-126">A sample for specifying hello `Hostname` and hello `credspec` in hello application manifest is shown in hello following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="edd7c-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="edd7c-127">Next steps</span></span>

* [<span data-ttu-id="edd7c-128">部署 Windows 容器 tooService 網狀架構上 Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="edd7c-128">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="edd7c-129">部署 Docker 容器 tooService Linux 上的網狀架構</span><span class="sxs-lookup"><span data-stu-id="edd7c-129">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
