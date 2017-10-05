---
title: "開始使用 Azure Service Fabric XPlat CLI"
description: "開始使用 Azure Service Fabric XPlat CLI"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: ddf881f6c202a82a3f64773639aa29b660057f8d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-xplat-cli-to-interact-with-a-service-fabric-cluster"></a><span data-ttu-id="356e7-103">使用 XPlat CLI 與 Service Fabric 叢集進行互動</span><span class="sxs-lookup"><span data-stu-id="356e7-103">Using the XPlat CLI to interact with a Service Fabric cluster</span></span>

<span data-ttu-id="356e7-104">您可以使用 Linux 上的 XPlat CLI，從 Linux 機器與 Service Fabric 叢集進行互動。</span><span class="sxs-lookup"><span data-stu-id="356e7-104">You can interact with Service Fabric cluster from Linux machines using the XPlat CLI on Linux.</span></span>

<span data-ttu-id="356e7-105">第一個步驟是從 git rep 取得最新版本的 CLI，並使用下列命令將它設定在您的路徑中︰</span><span class="sxs-lookup"><span data-stu-id="356e7-105">The first step is get the latest version of the CLI from the git rep and set it up in your path using the following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="356e7-106">對於它支援的每個命令，您可以輸入命令的名稱以取得該命令的說明。</span><span class="sxs-lookup"><span data-stu-id="356e7-106">For each command, it supports, you can type the name of the command to obtain the help for that command.</span></span>
<span data-ttu-id="356e7-107">支援自動完成命令。</span><span class="sxs-lookup"><span data-stu-id="356e7-107">Auto-completion is supported for the commands.</span></span> <span data-ttu-id="356e7-108">例如，下列命令可讓您取得所有應用程式命令的說明。</span><span class="sxs-lookup"><span data-stu-id="356e7-108">For example, the following command gives you help for all the application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="356e7-109">您可以進一步篩選出特定命令的說明，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="356e7-109">You can further filter the help to a specific command, as the following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="356e7-110">若要在 CLI 中啟用自動完成，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="356e7-110">To enable auto-completion in the CLI, run the following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="356e7-111">下列命令會連線到叢集，並顯示叢集中的節點︰</span><span class="sxs-lookup"><span data-stu-id="356e7-111">The following commands connect to the cluster and show you the nodes in the cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="356e7-112">若要使用具名參數並了解其用途，您可以在命令後面輸入 --help。</span><span class="sxs-lookup"><span data-stu-id="356e7-112">To use named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="356e7-113">例如：</span><span class="sxs-lookup"><span data-stu-id="356e7-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="356e7-114">從 **不屬於叢集**的電腦連接到多電腦叢集時，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="356e7-114">When connecting to a multi-machine cluster from a machine **that is not part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="356e7-115">適當地以實際 IP 或 FQDN 取代 PublicIPorFQDN 標記。</span><span class="sxs-lookup"><span data-stu-id="356e7-115">Replace the PublicIPorFQDN tag with the real IP or FQDN as appropriate.</span></span> <span data-ttu-id="356e7-116">從 **屬於叢集**的電腦連接到多電腦叢集時，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="356e7-116">When connecting to a multi-machine cluster from a machine **that is part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="356e7-117">您可以使用 PowerShell 或 CLI，與透過 Azure 入口網站建立的 Linux Service Fabric 叢集互動。</span><span class="sxs-lookup"><span data-stu-id="356e7-117">You can use PowerShell or CLI to interact with your Linux Service Fabric Cluster created through the Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="356e7-118">這些叢集不安全，因此，您可能因為在叢集資訊清單中新增公用 IP 位址，而造成單機系統門戶洞開。</span><span class="sxs-lookup"><span data-stu-id="356e7-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding the public IP address in the cluster manifest.</span></span>

## <a name="using-the-xplat-cli-to-connect-to-a-service-fabric-cluster"></a><span data-ttu-id="356e7-119">使用 XPlat CLI 來連線至 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="356e7-119">Using the XPlat CLI to connect to a Service Fabric cluster</span></span>

<span data-ttu-id="356e7-120">下列 Azure CLI 命令說明如何連線到安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="356e7-120">The following Azure CLI commands describe how to connect to a secure cluster.</span></span> <span data-ttu-id="356e7-121">憑證詳細資料必須與叢集節點上的憑證相符。</span><span class="sxs-lookup"><span data-stu-id="356e7-121">The certificate details must match a certificate on the cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="356e7-122">如果您的憑證有憑證授權單位 (CA)，則您需要新增 --ca-cert-path 參數，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="356e7-122">If your certificate has Certificate Authorities (CAs), you need to add the --ca-cert-path parameter like the following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="356e7-123">如果您有多個 CA，請使用逗號做為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="356e7-123">If you have multiple CAs, use a comma as the delimiter.</span></span>

<span data-ttu-id="356e7-124">如果憑證中的一般名稱不符合連接端點，您可以使用 `--strict-ssl-false` 參數略過驗證，如下列命令所示︰</span><span class="sxs-lookup"><span data-stu-id="356e7-124">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification as shown in the following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="356e7-125">如果您想要略過 CA 驗證，您可以新增 --reject-unauthorized-false 參數，如下列命令所示︰</span><span class="sxs-lookup"><span data-stu-id="356e7-125">If you would like to skip the CA verification, you could add the --reject-unauthorized-false parameter as shown in the following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="356e7-126">連線之後，您應該能夠執行其他 CLI 命令來與叢集互動。</span><span class="sxs-lookup"><span data-stu-id="356e7-126">After you connect, you should be able to run other CLI commands to interact with the cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="356e7-127">部署 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="356e7-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="356e7-128">執行下列命令來複製、註冊和啟動 Service Fabric 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="356e7-128">Execute the following commands to copy, register, and start the service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="356e7-129">升級您的應用程式</span><span class="sxs-lookup"><span data-stu-id="356e7-129">Upgrading your application</span></span>

<span data-ttu-id="356e7-130">處理程序類似於 [Windows 中的處理程序](service-fabric-application-upgrade-tutorial-powershell.md))。</span><span class="sxs-lookup"><span data-stu-id="356e7-130">The process is similar to the [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="356e7-131">從專案根目錄中建置、複製、註冊和建立您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="356e7-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="356e7-132">如果您的應用程式執行個體名為 `fabric:/MySFApp`，且類型為 MySFApp，則命令會如下所示︰</span><span class="sxs-lookup"><span data-stu-id="356e7-132">If your application instance is named `fabric:/MySFApp`, and the type is MySFApp, the commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="356e7-133">變更您的應用程式，並重建已修改的服務。</span><span class="sxs-lookup"><span data-stu-id="356e7-133">Make the change to your application and rebuild the modified service.</span></span>  <span data-ttu-id="356e7-134">以服務 (和程式碼或組態或資料，視情況而定) 已更新的版本，更新已修改之服務的資訊清單檔案 (ServiceManifest.xml)。</span><span class="sxs-lookup"><span data-stu-id="356e7-134">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="356e7-135">同時，也以應用程式已更新的版本號碼及已修改的服務，修改應用程式的資訊清單 (ApplicationManifest.xml)。</span><span class="sxs-lookup"><span data-stu-id="356e7-135">Also modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application, and the modified service.</span></span>  <span data-ttu-id="356e7-136">現在，使用下列命令來複製並註冊已更新的應用程式︰</span><span class="sxs-lookup"><span data-stu-id="356e7-136">Now, copy and register your updated application using the following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="356e7-137">現在，您可以使用下列命令來啟動應用程式升級︰</span><span class="sxs-lookup"><span data-stu-id="356e7-137">Now, you can start the application upgrade with the following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="356e7-138">您現在可以使用 SFX 來監視應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="356e7-138">You can now monitor the application upgrade using SFX.</span></span> <span data-ttu-id="356e7-139">應用程式在幾分鐘內會完成更新。</span><span class="sxs-lookup"><span data-stu-id="356e7-139">In a few minutes, the application would have been updated.</span></span> <span data-ttu-id="356e7-140">您也可以用錯誤動作來測試已更新的應用程式，並檢查 Service Fabric 中的自動回復功能。</span><span class="sxs-lookup"><span data-stu-id="356e7-140">You can also try an updated app with an error and check the auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a><span data-ttu-id="356e7-141">從 PFX 轉換為 PEM (反之亦然)</span><span class="sxs-lookup"><span data-stu-id="356e7-141">Converting from PFX to PEM and vice versa</span></span>

<span data-ttu-id="356e7-142">您可能需要在本機電腦 (採用 Windows 或 Linux) 上安裝憑證，以存取可能位於不同環境中的安全叢集。</span><span class="sxs-lookup"><span data-stu-id="356e7-142">You might need to install a certificate in your local machine (with Windows or Linux) to access secure clusters that may be in a different environment.</span></span> <span data-ttu-id="356e7-143">比方說，從 Windows 電腦存取安全的 Linux 叢集 (反之亦然) 時，您可能需要將憑證從 PFX 轉換為 PEM。</span><span class="sxs-lookup"><span data-stu-id="356e7-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need to convert your certificate from PFX to PEM and vice versa.</span></span> 

<span data-ttu-id="356e7-144">若要從 PEM 檔案轉換為 PFX 檔案，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="356e7-144">To convert from a PEM file to a PFX file, use the following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="356e7-145">若要從 PFX 檔案轉換為 PEM 檔案，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="356e7-145">To convert from a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="356e7-146">請參閱[OpenSSL 文件](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html)以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="356e7-146">Refer to [OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="356e7-147">疑難排解</span><span class="sxs-lookup"><span data-stu-id="356e7-147">Troubleshooting</span></span>


### <a name="copying-of-the-application-package-does-not-succeed"></a><span data-ttu-id="356e7-148">未成功複製應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="356e7-148">Copying of the application package does not succeed</span></span>

<span data-ttu-id="356e7-149">檢查是否已安裝 `openssh` 。</span><span class="sxs-lookup"><span data-stu-id="356e7-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="356e7-150">根據預設，Ubuntu 桌面不會安裝此軟體。</span><span class="sxs-lookup"><span data-stu-id="356e7-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="356e7-151">使用下列命令安裝它：</span><span class="sxs-lookup"><span data-stu-id="356e7-151">Install it using the following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="356e7-152">如果問題持續發生，請使用下列命令來變更 `sshd_config` 檔案，以嘗試對 ssh 停用 PAM：</span><span class="sxs-lookup"><span data-stu-id="356e7-152">If the problem persists, try disabling PAM for ssh by changing the `sshd_config` file using the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="356e7-153">如果問題還是持續發生，請執行下列命令來嘗試增加 ssh 工作階段數目︰</span><span class="sxs-lookup"><span data-stu-id="356e7-153">If the problem still persists, try increasing the number of ssh sessions by executing the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="356e7-154">尚不支援使用金鑰 (而不是密碼) 進行 ssh 驗證 (因為平台會使用 ssh 來複製套件)，請改為使用密碼驗證。</span><span class="sxs-lookup"><span data-stu-id="356e7-154">Using keys for ssh authentication (as opposed to passwords) isn't yet supported (since the platform uses ssh to copy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="356e7-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="356e7-155">Next steps</span></span>

[<span data-ttu-id="356e7-156">設定開發環境，並將 Service Fabric 應用程式部署到 Linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="356e7-156">Set up the development environment and deploy a Service Fabric application to a Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="356e7-157">相關文章</span><span class="sxs-lookup"><span data-stu-id="356e7-157">Related articles</span></span>

* [<span data-ttu-id="356e7-158">開始使用 Service Fabric 和 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="356e7-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
