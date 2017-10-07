---
title: "開始使用 Azure Service Fabric 和 Azure CLI 2.0 aaaGet"
description: "了解 toouse hello Azure Service Fabric 命令如何在 Azure CLI 2.0 版中的模組。 深入了解如何 tooconnect tooa 叢集，以及如何 toomanage 應用程式。"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="7e648-104">Azure Service Fabric 和 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7e648-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="7e648-105">hello Azure 命令列工具 (Azure CLI) 2.0 版包含命令 toohelp 您管理 Azure Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="7e648-105">hello Azure command-line tool (Azure CLI) version 2.0 includes commands toohelp you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="7e648-106">了解 tooget 如何開始使用 Azure CLI 和服務網狀架構。</span><span class="sxs-lookup"><span data-stu-id="7e648-106">Learn how tooget started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="7e648-107">安裝 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7e648-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="7e648-108">您可以使用 Azure CLI 2.0 命令 toointeract 與和管理 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="7e648-108">You can use Azure CLI 2.0 commands toointeract with and manage Service Fabric clusters.</span></span> <span data-ttu-id="7e648-109">tooget hello 最新版本的 Azure CLI，後續 hello [Azure CLI 2.0 標準安裝程序](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="7e648-109">tooget hello latest version of Azure CLI, follow hello [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="7e648-110">如需詳細資訊，請參閱 hello [Azure CLI 2.0 概觀](https://docs.microsoft.com/en-us/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7e648-110">For more information, see hello [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="7e648-111">Azure CLI 語法</span><span class="sxs-lookup"><span data-stu-id="7e648-111">Azure CLI syntax</span></span>

<span data-ttu-id="7e648-112">在 Azure CLI 中，所有 Service Fabric 命令前面都會加上 `az sf`。</span><span class="sxs-lookup"><span data-stu-id="7e648-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="7e648-113">您可以使用 hello 命令的相關的一般資訊，請使用`az sf -h`。</span><span class="sxs-lookup"><span data-stu-id="7e648-113">For general information about hello commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="7e648-114">如需單一命令的說明，請使用 `az sf <command> -h`。</span><span class="sxs-lookup"><span data-stu-id="7e648-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="7e648-115">Azure CLI 中的 Service Fabric 命令會遵循此命名模式：</span><span class="sxs-lookup"><span data-stu-id="7e648-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="7e648-116">`<object>`是 hello 目標`<action>`。</span><span class="sxs-lookup"><span data-stu-id="7e648-116">`<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="7e648-117">選取叢集</span><span class="sxs-lookup"><span data-stu-id="7e648-117">Select a cluster</span></span>

<span data-ttu-id="7e648-118">在執行任何作業之前，您必須選取要叢集 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="7e648-118">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="7e648-119">如需範例，請參閱下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="7e648-119">For an example, see hello following code.</span></span> <span data-ttu-id="7e648-120">hello 程式碼連接 tooan 不安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="7e648-120">hello code connects tooan unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="7e648-121">請勿於生產環境中使用不安全的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="7e648-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="7e648-122">hello 叢集端點都必須加`http`或`https`。</span><span class="sxs-lookup"><span data-stu-id="7e648-122">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="7e648-123">它必須包括 hello hello HTTP 閘道的連接埠。</span><span class="sxs-lookup"><span data-stu-id="7e648-123">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="7e648-124">hello 連接埠和位址都 hello 與 hello Service Fabric 總管 URL 相同。</span><span class="sxs-lookup"><span data-stu-id="7e648-124">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="7e648-125">對於使用憑證保護的叢集，您可以使用未加密的 .pem 檔案或 .crt 和 .key 檔案。</span><span class="sxs-lookup"><span data-stu-id="7e648-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="7e648-126">例如：</span><span class="sxs-lookup"><span data-stu-id="7e648-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="7e648-127">如需詳細資訊，請參閱[連接 tooa 安全 Azure Service Fabric 叢集](service-fabric-connect-to-secure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="7e648-127">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7e648-128">hello`select`之前它會傳回命令不會處理任何要求。</span><span class="sxs-lookup"><span data-stu-id="7e648-128">hello `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="7e648-129">您所指定的叢集是否正確，tooverify 使用類似的命令`az sf cluster health`。</span><span class="sxs-lookup"><span data-stu-id="7e648-129">tooverify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="7e648-130">請確認 hello 命令不會傳回任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="7e648-130">Verify that hello command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="7e648-131">基本作業</span><span class="sxs-lookup"><span data-stu-id="7e648-131">Basic operations</span></span>

<span data-ttu-id="7e648-132">叢集連線資訊會跨多個 Azure CLI 工作階段保存。</span><span class="sxs-lookup"><span data-stu-id="7e648-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="7e648-133">選取 Service Fabric 叢集之後，您可以在 hello 叢集上執行任何 Service Fabric 命令。</span><span class="sxs-lookup"><span data-stu-id="7e648-133">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="7e648-134">比方說，tooget hello Service Fabric 叢集健全狀況狀態，會使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e648-134">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="7e648-135">hello 命令會產生 hello 下列輸出 （假設 hello Azure CLI 組態中所指定 JSON 輸出）：</span><span class="sxs-lookup"><span data-stu-id="7e648-135">hello command results in hello following output (assuming that JSON output is specified in hello Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="7e648-136">秘訣與疑難排解</span><span class="sxs-lookup"><span data-stu-id="7e648-136">Tips and troubleshooting</span></span>

<span data-ttu-id="7e648-137">您可能會發現您在使用 Azure CLI Service Fabric 命令時遇到問題時，下列資訊很有幫助的 hello。</span><span class="sxs-lookup"><span data-stu-id="7e648-137">You might find hello following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="7e648-138">將憑證從 PFX tooPEM 格式轉換</span><span class="sxs-lookup"><span data-stu-id="7e648-138">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="7e648-139">Azure CLI 支援以 PEM (.pem 副檔名) 檔案作為用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="7e648-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="7e648-140">如果您從 Windows 使用 PFX 檔案，您必須將這些憑證 tooPEM 格式轉換。</span><span class="sxs-lookup"><span data-stu-id="7e648-140">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="7e648-141">tooconvert PFX 檔案 tooa PEM 檔案，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e648-141">tooconvert a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="7e648-142">如需詳細資訊，請參閱 hello [OpenSSL 文件](https://www.openssl.org/docs/)。</span><span class="sxs-lookup"><span data-stu-id="7e648-142">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="7e648-143">連接問題</span><span class="sxs-lookup"><span data-stu-id="7e648-143">Connection issues</span></span>

<span data-ttu-id="7e648-144">某些作業可能會產生下列訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e648-144">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="7e648-145">請確認該 hello 可讓您指定叢集端點可供使用和接聽。</span><span class="sxs-lookup"><span data-stu-id="7e648-145">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="7e648-146">此外，請確認該 hello Service Fabric 總管 UI 位於的主機和連接埠。</span><span class="sxs-lookup"><span data-stu-id="7e648-146">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="7e648-147">tooupdate hello 端點，使用`az sf cluster select`。</span><span class="sxs-lookup"><span data-stu-id="7e648-147">tooupdate hello endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="7e648-148">詳細記錄</span><span class="sxs-lookup"><span data-stu-id="7e648-148">Detailed logs</span></span>

<span data-ttu-id="7e648-149">當您偵錯或回報問題時，詳細記錄通常很有幫助。</span><span class="sxs-lookup"><span data-stu-id="7e648-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="7e648-150">Azure CLI 提供全域`--debug`旗標，會增加 hello 的記錄檔的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7e648-150">Azure CLI offers a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="7e648-151">命令的說明和語法</span><span class="sxs-lookup"><span data-stu-id="7e648-151">Command help and syntax</span></span>

<span data-ttu-id="7e648-152">Service Fabric 命令後續 hello Azure CLI 為相同的慣例。</span><span class="sxs-lookup"><span data-stu-id="7e648-152">Service Fabric commands follow hello same conventions as Azure CLI.</span></span> <span data-ttu-id="7e648-153">與特定命令或一組命令的說明，請使用 hello`-h`旗標：</span><span class="sxs-lookup"><span data-stu-id="7e648-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="7e648-154">以下是另一個範例︰</span><span class="sxs-lookup"><span data-stu-id="7e648-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
