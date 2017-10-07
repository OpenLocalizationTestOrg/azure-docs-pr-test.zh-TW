---
title: "開始使用 Azure Service Fabric XPlat CLI aaaGetting"
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
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a><span data-ttu-id="b890c-103">Hello XPlat CLI toointeract 使用 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="b890c-103">Using hello XPlat CLI toointeract with a Service Fabric cluster</span></span>

<span data-ttu-id="b890c-104">您可以互動 Linux 機器，在 Linux 上使用 hello XPlat CLI 從 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="b890c-104">You can interact with Service Fabric cluster from Linux machines using hello XPlat CLI on Linux.</span></span>

<span data-ttu-id="b890c-105">hello 第一個步驟是取得 hello CLI hello 最新版本，從 hello git rep 並設定它在路徑中使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="b890c-105">hello first step is get hello latest version of hello CLI from hello git rep and set it up in your path using hello following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="b890c-106">每個命令，它支援，您可以輸入 hello 名稱 hello 命令 tooobtain hello 說明該命令。</span><span class="sxs-lookup"><span data-stu-id="b890c-106">For each command, it supports, you can type hello name of hello command tooobtain hello help for that command.</span></span>
<span data-ttu-id="b890c-107">Hello 命令支援自動完成。</span><span class="sxs-lookup"><span data-stu-id="b890c-107">Auto-completion is supported for hello commands.</span></span> <span data-ttu-id="b890c-108">例如，hello 下列命令可讓您所有的 hello 應用程式命令的說明。</span><span class="sxs-lookup"><span data-stu-id="b890c-108">For example, hello following command gives you help for all hello application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="b890c-109">您可以為下列範例所示的 hello 進一步篩選 hello 說明 tooa 特定命令：</span><span class="sxs-lookup"><span data-stu-id="b890c-109">You can further filter hello help tooa specific command, as hello following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="b890c-110">tooenable 的自動完成 hello CLI，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b890c-110">tooenable auto-completion in hello CLI, run hello following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="b890c-111">下列命令的 hello 連接 toohello 叢集並顯示 hello hello 叢集中的節點：</span><span class="sxs-lookup"><span data-stu-id="b890c-111">hello following commands connect toohello cluster and show you hello nodes in hello cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="b890c-112">toouse 具名參數，而且找出它們的是，您可以輸入-說明命令之後。</span><span class="sxs-lookup"><span data-stu-id="b890c-112">toouse named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="b890c-113">例如：</span><span class="sxs-lookup"><span data-stu-id="b890c-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="b890c-114">從機器連接 tooa 多電腦叢集時**也就是未叢集的一部分 hello**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b890c-114">When connecting tooa multi-machine cluster from a machine **that is not part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="b890c-115">取代為 hello PublicIPorFQDN 標記 hello 實際 IP 或 FQDN 適當。</span><span class="sxs-lookup"><span data-stu-id="b890c-115">Replace hello PublicIPorFQDN tag with hello real IP or FQDN as appropriate.</span></span> <span data-ttu-id="b890c-116">從機器連接 tooa 多電腦叢集時**也就是叢集一部分的 hello**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b890c-116">When connecting tooa multi-machine cluster from a machine **that is part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="b890c-117">您可以使用 PowerShell 或 CLI toointeract 與您的 Linux Service Fabric 叢集建立透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b890c-117">You can use PowerShell or CLI toointeract with your Linux Service Fabric Cluster created through hello Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="b890c-118">這些叢集不安全，因此，您可能會開啟一個方塊在 hello 叢集資訊清單中加入 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b890c-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding hello public IP address in hello cluster manifest.</span></span>

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a><span data-ttu-id="b890c-119">使用 hello XPlat CLI tooconnect tooa Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="b890c-119">Using hello XPlat CLI tooconnect tooa Service Fabric cluster</span></span>

<span data-ttu-id="b890c-120">下列 Azure CLI 命令的 hello 說明 tooconnect tooa 如何保護叢集。</span><span class="sxs-lookup"><span data-stu-id="b890c-120">hello following Azure CLI commands describe how tooconnect tooa secure cluster.</span></span> <span data-ttu-id="b890c-121">hello 憑證詳細資料必須符合 hello 叢集節點上的憑證。</span><span class="sxs-lookup"><span data-stu-id="b890c-121">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="b890c-122">如果您的憑證的憑證授權單位 (Ca)，您會需要 tooadd hello-ca 憑證路徑參數，如下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="b890c-122">If your certificate has Certificate Authorities (CAs), you need tooadd hello --ca-cert-path parameter like hello following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="b890c-123">如果您有多個 Ca，請使用逗號做為 hello 分隔符號。</span><span class="sxs-lookup"><span data-stu-id="b890c-123">If you have multiple CAs, use a comma as hello delimiter.</span></span>

<span data-ttu-id="b890c-124">如果您在 hello 憑證的一般名稱不符合 hello 連接端點，您可以使用 hello 參數`--strict-ssl-false`toobypass hello 驗證，下列命令的 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="b890c-124">If your Common Name in hello certificate does not match hello connection endpoint, you could use hello parameter `--strict-ssl-false` toobypass hello verification as shown in hello following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="b890c-125">如果您想要 tooskip hello CA 驗證，您可以加入 hello-拒絕未經授權的 false 參數 hello 下列命令所示：</span><span class="sxs-lookup"><span data-stu-id="b890c-125">If you would like tooskip hello CA verification, you could add hello --reject-unauthorized-false parameter as shown in hello following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="b890c-126">您連接之後，您應該能夠 toorun 與其他 CLI 命令 toointeract hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b890c-126">After you connect, you should be able toorun other CLI commands toointeract with hello cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="b890c-127">部署 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="b890c-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="b890c-128">執行下列命令 toocopy，註冊，並啟動 hello service fabric 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="b890c-128">Execute hello following commands toocopy, register, and start hello service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="b890c-129">升級您的應用程式</span><span class="sxs-lookup"><span data-stu-id="b890c-129">Upgrading your application</span></span>

<span data-ttu-id="b890c-130">hello 程序是類似 toohello [windows 處理序](service-fabric-application-upgrade-tutorial-powershell.md))。</span><span class="sxs-lookup"><span data-stu-id="b890c-130">hello process is similar toohello [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="b890c-131">從專案根目錄中建置、複製、註冊和建立您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b890c-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="b890c-132">如果您的應用程式執行個體的名稱為`fabric:/MySFApp`，hello 類型和 MySFApp，hello 命令應如下：</span><span class="sxs-lookup"><span data-stu-id="b890c-132">If your application instance is named `fabric:/MySFApp`, and hello type is MySFApp, hello commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="b890c-133">請變更 tooyour 應用程式，並重建 hello 修改服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="b890c-133">Make hello change tooyour application and rebuild hello modified service.</span></span>  <span data-ttu-id="b890c-134">更新 hello 修改服務的資訊清單檔案 (ServiceManifest.xml) 與 hello 更新版本的 hello 服務 （和程式碼或組態或視需要的資料）。</span><span class="sxs-lookup"><span data-stu-id="b890c-134">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="b890c-135">也具有 hello 更新的版本號碼 hello 應用程式中，修改 hello 應用程式資訊清單 (ApplicationManifest.xml) 和 hello 已修改的服務。</span><span class="sxs-lookup"><span data-stu-id="b890c-135">Also modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application, and hello modified service.</span></span>  <span data-ttu-id="b890c-136">現在，複製並註冊您更新的應用程式，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b890c-136">Now, copy and register your updated application using hello following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="b890c-137">現在，您可以使用下列命令的 hello 啟動 hello 應用程式升級：</span><span class="sxs-lookup"><span data-stu-id="b890c-137">Now, you can start hello application upgrade with hello following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="b890c-138">您現在可以監視使用 SFX hello 應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="b890c-138">You can now monitor hello application upgrade using SFX.</span></span> <span data-ttu-id="b890c-139">在幾分鐘的時間，hello 應用程式會有更新。</span><span class="sxs-lookup"><span data-stu-id="b890c-139">In a few minutes, hello application would have been updated.</span></span> <span data-ttu-id="b890c-140">您也可以再試一次更新應用程式，但發生錯誤，並檢查服務網狀架構中的 hello 自動回復功能。</span><span class="sxs-lookup"><span data-stu-id="b890c-140">You can also try an updated app with an error and check hello auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-toopem-and-vice-versa"></a><span data-ttu-id="b890c-141">轉換從 PFX tooPEM 反之亦然</span><span class="sxs-lookup"><span data-stu-id="b890c-141">Converting from PFX tooPEM and vice versa</span></span>

<span data-ttu-id="b890c-142">您本機電腦 （具有 Windows 或 Linux） tooaccess 安全叢集中可能在不同的環境中，您可能需要 tooinstall 憑證。</span><span class="sxs-lookup"><span data-stu-id="b890c-142">You might need tooinstall a certificate in your local machine (with Windows or Linux) tooaccess secure clusters that may be in a different environment.</span></span> <span data-ttu-id="b890c-143">例如，存取受保護的 Linux 叢集從 Windows 電腦，反之亦然時您可能需要 tooconvert 憑證從 PFX tooPEM，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="b890c-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need tooconvert your certificate from PFX tooPEM and vice versa.</span></span> 

<span data-ttu-id="b890c-144">從 PEM 檔案 tooa PFX 檔案，下列命令使用 hello tooconvert:</span><span class="sxs-lookup"><span data-stu-id="b890c-144">tooconvert from a PEM file tooa PFX file, use hello following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="b890c-145">從 PFX 檔案 tooa PEM 檔案，下列命令使用 hello tooconvert:</span><span class="sxs-lookup"><span data-stu-id="b890c-145">tooconvert from a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="b890c-146">請參閱太[OpenSSL 文件](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b890c-146">Refer too[OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="b890c-147">疑難排解</span><span class="sxs-lookup"><span data-stu-id="b890c-147">Troubleshooting</span></span>


### <a name="copying-of-hello-application-package-does-not-succeed"></a><span data-ttu-id="b890c-148">未成功複製的 hello 應用程式套件</span><span class="sxs-lookup"><span data-stu-id="b890c-148">Copying of hello application package does not succeed</span></span>

<span data-ttu-id="b890c-149">檢查是否已安裝 `openssh` 。</span><span class="sxs-lookup"><span data-stu-id="b890c-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="b890c-150">根據預設，Ubuntu 桌面不會安裝此軟體。</span><span class="sxs-lookup"><span data-stu-id="b890c-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="b890c-151">使用安裝 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="b890c-151">Install it using hello following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="b890c-152">如果 hello 問題持續發生，請嘗試停用的 PAM ssh 藉由變更 hello`sshd_config`檔案使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b890c-152">If hello problem persists, try disabling PAM for ssh by changing hello `sshd_config` file using hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="b890c-153">如果 hello 問題持續發生，請嘗試 hello 日益增加的 ssh 工作階段藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b890c-153">If hello problem still persists, try increasing hello number of ssh sessions by executing hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="b890c-154">使用金鑰的 ssh 驗證 （做為相對於 toopasswords) 尚不支援 （因為 hello 平台會使用 ssh toocopy 封裝），因此改為使用密碼驗證。</span><span class="sxs-lookup"><span data-stu-id="b890c-154">Using keys for ssh authentication (as opposed toopasswords) isn't yet supported (since hello platform uses ssh toocopy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b890c-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b890c-155">Next steps</span></span>

[<span data-ttu-id="b890c-156">設定 hello 開發環境和部署 Service Fabric 應用程式 tooa Linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="b890c-156">Set up hello development environment and deploy a Service Fabric application tooa Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="b890c-157">相關文章</span><span class="sxs-lookup"><span data-stu-id="b890c-157">Related articles</span></span>

* [<span data-ttu-id="b890c-158">開始使用 Service Fabric 和 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b890c-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
