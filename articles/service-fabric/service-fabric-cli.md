---
title: "開始使用 Azure Service Fabric CLI (sfctl) aaaGet"
description: "了解如何 toouse hello Azure Service Fabric CLI。 深入了解如何 tooconnect tooa 叢集，以及如何 toomanage 應用程式。"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="bd8ff-104">Azure Service Fabric 命令列</span><span class="sxs-lookup"><span data-stu-id="bd8ff-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="bd8ff-105">hello Azure Service Fabric CLI (sfctl) 是命令列公用程式互動，及管理 Azure Service Fabric 實體。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-105">hello Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="bd8ff-106">Sfctl 可以搭配 Windows 或 Linux 叢集使用。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="bd8ff-107">Sfctl 可在支援 python 的任何平台上執行。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd8ff-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="bd8ff-108">Prerequisites</span></span>

<span data-ttu-id="bd8ff-109">先前 tooinstallation，請確定您的環境具有 python 和安裝的 pip。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-109">Prior tooinstallation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="bd8ff-110">如需詳細資訊，看看 hello [pip 快速入門文件](https://pip.pypa.io/en/latest/quickstart/)，和官方[python 安裝文件集](https://wiki.python.org/moin/BeginnersGuide/Download)。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-110">For more information, take a look at hello [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="bd8ff-111">雖然這兩個 python 2.7 和 3.6 受到支援，但建議 toouse python 3.6。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-111">While both python 2.7 and 3.6 are supported, it is recommended toouse python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="bd8ff-112">Install</span><span class="sxs-lookup"><span data-stu-id="bd8ff-112">Install</span></span>

<span data-ttu-id="bd8ff-113">hello Azure Service Fabric CLI (sfctl) 會封裝成 python 封裝。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-113">hello Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="bd8ff-114">tooinstall hello 最新版本執行：</span><span class="sxs-lookup"><span data-stu-id="bd8ff-114">tooinstall hello latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="bd8ff-115">安裝之後，執行`sfctl -h`tooget 可用命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-115">After installation, run `sfctl -h` tooget information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="bd8ff-116">CLI 語法</span><span class="sxs-lookup"><span data-stu-id="bd8ff-116">CLI syntax</span></span>

<span data-ttu-id="bd8ff-117">命令前面一律會加上 `sfctl`。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="bd8ff-118">如需有關所有命令的一般資訊，請使用 `sfctl -h`。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="bd8ff-119">如需單一命令的說明，請使用 `sfctl <command> -h`。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="bd8ff-120">命令後續可重複結構，與 hello 目標的 hello 命令前面的動作或 hello 動詞命令：</span><span class="sxs-lookup"><span data-stu-id="bd8ff-120">Commands follow a repeatable structure, with hello target of hello command preceding hello verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="bd8ff-121">在此範例中， `<object>` hello 的目標`<action>`。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-121">In this example, `<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="bd8ff-122">選取叢集</span><span class="sxs-lookup"><span data-stu-id="bd8ff-122">Select a cluster</span></span>

<span data-ttu-id="bd8ff-123">在執行任何作業之前，您必須選取要叢集 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-123">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="bd8ff-124">比方說，執行下列 tooselect hello 和連接 hello 名稱 toohello 叢集`testcluster.com`。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-124">For example, run hello following tooselect and connect toohello cluster with hello name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="bd8ff-125">請勿於生產環境中使用不安全的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="bd8ff-126">hello 叢集端點都必須加`http`或`https`。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-126">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="bd8ff-127">它必須包括 hello hello HTTP 閘道的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-127">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="bd8ff-128">hello 連接埠和位址都 hello 與 hello Service Fabric 總管 URL 相同。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-128">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="bd8ff-129">對於使用憑證保護的叢集，您可以指定 PEM 編碼的憑證。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="bd8ff-130">hello 憑證可以指定為單一檔案或憑證和金鑰組。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-130">hello certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="bd8ff-131">如需詳細資訊，請參閱[連接 tooa 安全 Azure Service Fabric 叢集](service-fabric-connect-to-secure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-131">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="bd8ff-132">基本作業</span><span class="sxs-lookup"><span data-stu-id="bd8ff-132">Basic operations</span></span>

<span data-ttu-id="bd8ff-133">叢集連線資訊會跨多個 sfctl 工作階段保存。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="bd8ff-134">選取 Service Fabric 叢集之後，您可以在 hello 叢集上執行任何 Service Fabric 命令。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-134">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="bd8ff-135">比方說，tooget hello Service Fabric 叢集健全狀況狀態，會使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="bd8ff-135">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="bd8ff-136">hello 命令會產生下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="bd8ff-136">hello command results in hello following output:</span></span>

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="bd8ff-137">秘訣與疑難排解</span><span class="sxs-lookup"><span data-stu-id="bd8ff-137">Tips and troubleshooting</span></span>

<span data-ttu-id="bd8ff-138">用於解決一般問題的某些建議和秘訣。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="bd8ff-139">將憑證從 PFX tooPEM 格式轉換</span><span class="sxs-lookup"><span data-stu-id="bd8ff-139">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="bd8ff-140">服務網狀架構 CLI hello 支援 PEM （副檔名為.pem） 檔案和用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-140">hello Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="bd8ff-141">如果您從 Windows 使用 PFX 檔案，您必須將這些憑證 tooPEM 格式轉換。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-141">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="bd8ff-142">tooconvert PFX 檔案 tooa PEM 檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="bd8ff-142">tooconvert a PFX file tooa PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="bd8ff-143">如需詳細資訊，請參閱 hello [OpenSSL 文件](https://www.openssl.org/docs/)。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-143">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="bd8ff-144">連接問題</span><span class="sxs-lookup"><span data-stu-id="bd8ff-144">Connection issues</span></span>

<span data-ttu-id="bd8ff-145">某些作業可能會產生下列訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="bd8ff-145">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="bd8ff-146">請確認該 hello 可讓您指定叢集端點可供使用和接聽。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-146">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="bd8ff-147">此外，請確認該 hello Service Fabric 總管 UI 位於的主機和連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-147">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="bd8ff-148">tooupdate hello 端點，使用`sfctl cluster select`。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-148">tooupdate hello endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="bd8ff-149">詳細記錄</span><span class="sxs-lookup"><span data-stu-id="bd8ff-149">Detailed logs</span></span>

<span data-ttu-id="bd8ff-150">當您偵錯或回報問題時，詳細記錄通常很有幫助。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="bd8ff-151">沒有全域`--debug`旗標，會增加 hello 的記錄檔的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bd8ff-151">There is a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="bd8ff-152">命令的說明和語法</span><span class="sxs-lookup"><span data-stu-id="bd8ff-152">Command help and syntax</span></span>

<span data-ttu-id="bd8ff-153">與特定命令或一組命令的說明，請使用 hello`-h`旗標：</span><span class="sxs-lookup"><span data-stu-id="bd8ff-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="bd8ff-154">另一個範例：</span><span class="sxs-lookup"><span data-stu-id="bd8ff-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="bd8ff-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd8ff-155">Next steps</span></span>

* [<span data-ttu-id="bd8ff-156">部署應用程式以 hello Azure Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="bd8ff-156">Deploy an application with hello Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="bd8ff-157">在 Linux 上開始使用 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bd8ff-157">Get started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
