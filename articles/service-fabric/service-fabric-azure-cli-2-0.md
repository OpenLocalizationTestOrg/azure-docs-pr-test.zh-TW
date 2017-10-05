---
title: "開始使用 Azure Service Fabric 和 Azure CLI 2.0"
description: "了解如何在 Azure CLI 2.0 版中使用 Azure Service Fabric 命令模組。 了解如何連線到叢集，以及如何管理應用程式。"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ee3302b984ca2f5509755dc17b0a5fd06ace0afe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="3c98f-104">Azure Service Fabric 和 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3c98f-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="3c98f-105">Azure 命令列工具 (Azure CLI) 2.0 版包含可協助您管理 Azure Service Fabric 叢集的命令。</span><span class="sxs-lookup"><span data-stu-id="3c98f-105">The Azure command-line tool (Azure CLI) version 2.0 includes commands to help you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="3c98f-106">了解如何開始使用 Azure Service Fabric 和 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="3c98f-106">Learn how to get started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="3c98f-107">安裝 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3c98f-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="3c98f-108">您可以使用 Azure CLI 2.0 命令來與 Service Fabric 叢集互動和進行管理。</span><span class="sxs-lookup"><span data-stu-id="3c98f-108">You can use Azure CLI 2.0 commands to interact with and manage Service Fabric clusters.</span></span> <span data-ttu-id="3c98f-109">若要取得最新版的 Azure CLI，請遵循 [Azure CLI 2.0 標準安裝程序](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="3c98f-109">To get the latest version of Azure CLI, follow the [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="3c98f-110">如需詳細資訊，請參閱 [Azure CLI 2.0 概觀](https://docs.microsoft.com/en-us/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="3c98f-110">For more information, see the [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="3c98f-111">Azure CLI 語法</span><span class="sxs-lookup"><span data-stu-id="3c98f-111">Azure CLI syntax</span></span>

<span data-ttu-id="3c98f-112">在 Azure CLI 中，所有 Service Fabric 命令前面都會加上 `az sf`。</span><span class="sxs-lookup"><span data-stu-id="3c98f-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="3c98f-113">如需有關可用命令的一般資訊，請使用 `az sf -h`。</span><span class="sxs-lookup"><span data-stu-id="3c98f-113">For general information about the commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="3c98f-114">如需單一命令的說明，請使用 `az sf <command> -h`。</span><span class="sxs-lookup"><span data-stu-id="3c98f-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="3c98f-115">Azure CLI 中的 Service Fabric 命令會遵循此命名模式：</span><span class="sxs-lookup"><span data-stu-id="3c98f-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="3c98f-116">`<object>` 是 `<action>` 的目標。</span><span class="sxs-lookup"><span data-stu-id="3c98f-116">`<object>` is the target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="3c98f-117">選取叢集</span><span class="sxs-lookup"><span data-stu-id="3c98f-117">Select a cluster</span></span>

<span data-ttu-id="3c98f-118">在您執行任何作業之前，必須選取要連線的叢集。</span><span class="sxs-lookup"><span data-stu-id="3c98f-118">Before you perform any operations, you must select a cluster to connect to.</span></span> <span data-ttu-id="3c98f-119">如需範例，請參閱下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="3c98f-119">For an example, see the following code.</span></span> <span data-ttu-id="3c98f-120">此程式碼會連線至不安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="3c98f-120">The code connects to an unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="3c98f-121">請勿於生產環境中使用不安全的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="3c98f-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="3c98f-122">叢集端點前面必須加上 `http` 或 `https`。</span><span class="sxs-lookup"><span data-stu-id="3c98f-122">The cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="3c98f-123">它必須包含 HTTP 閘道的連接埠。</span><span class="sxs-lookup"><span data-stu-id="3c98f-123">It must include the port for the HTTP gateway.</span></span> <span data-ttu-id="3c98f-124">此連接埠和位址等同於 Service Fabric Explorer URL。</span><span class="sxs-lookup"><span data-stu-id="3c98f-124">The port and address are the same as the Service Fabric Explorer URL.</span></span>

<span data-ttu-id="3c98f-125">對於使用憑證保護的叢集，您可以使用未加密的 .pem 檔案或 .crt 和 .key 檔案。</span><span class="sxs-lookup"><span data-stu-id="3c98f-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="3c98f-126">例如：</span><span class="sxs-lookup"><span data-stu-id="3c98f-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="3c98f-127">如需詳細資訊，請參閱[連線到 Azure Service Fabric 叢集](service-fabric-connect-to-secure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="3c98f-127">For more information, see [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3c98f-128">`select` 命令不會在要求傳回前採取動作。</span><span class="sxs-lookup"><span data-stu-id="3c98f-128">The `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="3c98f-129">若要確認您已正確指定叢集，請使用 `az sf cluster health` 之類的命令。</span><span class="sxs-lookup"><span data-stu-id="3c98f-129">To verify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="3c98f-130">確認此命令不會傳回任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="3c98f-130">Verify that the command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="3c98f-131">基本作業</span><span class="sxs-lookup"><span data-stu-id="3c98f-131">Basic operations</span></span>

<span data-ttu-id="3c98f-132">叢集連線資訊會跨多個 Azure CLI 工作階段保存。</span><span class="sxs-lookup"><span data-stu-id="3c98f-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="3c98f-133">選取 Service Fabric 叢集後，您可以在此叢集上執行任何 Service Fabric 命令。</span><span class="sxs-lookup"><span data-stu-id="3c98f-133">After you select a Service Fabric cluster, you can run any Service Fabric command on the cluster.</span></span>

<span data-ttu-id="3c98f-134">例如，若要取得 Service Fabric 叢集健康情況，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="3c98f-134">For example, to get the Service Fabric cluster health state, use the following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="3c98f-135">此命令會產生下列輸出 (假設已在 Azure CLI 組態中指定 JSON 輸出)：</span><span class="sxs-lookup"><span data-stu-id="3c98f-135">The command results in the following output (assuming that JSON output is specified in the Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="3c98f-136">秘訣與疑難排解</span><span class="sxs-lookup"><span data-stu-id="3c98f-136">Tips and troubleshooting</span></span>

<span data-ttu-id="3c98f-137">如果您在 Azure CLI 中使用 Service Fabric 命令時遇到問題，您會發現下列資訊很有幫助。</span><span class="sxs-lookup"><span data-stu-id="3c98f-137">You might find the following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a><span data-ttu-id="3c98f-138">將憑證從 PFX 轉換為 PEM 格式</span><span class="sxs-lookup"><span data-stu-id="3c98f-138">Convert a certificate from PFX to PEM format</span></span>

<span data-ttu-id="3c98f-139">Azure CLI 支援以 PEM (.pem 副檔名) 檔案作為用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="3c98f-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="3c98f-140">如果您從 Windows 使用 PFX 檔案，則必須將這些憑證轉換成 PEM 格式。</span><span class="sxs-lookup"><span data-stu-id="3c98f-140">If you use PFX files from Windows, you must convert those certificates to PEM format.</span></span> <span data-ttu-id="3c98f-141">若要將 PFX 檔案轉換為 PEM 檔案，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="3c98f-141">To convert a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="3c98f-142">如需詳細資訊，請參閱 [OpenSSL 文件](https://www.openssl.org/docs/)。</span><span class="sxs-lookup"><span data-stu-id="3c98f-142">For more information, see the [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="3c98f-143">連接問題</span><span class="sxs-lookup"><span data-stu-id="3c98f-143">Connection issues</span></span>

<span data-ttu-id="3c98f-144">某些作業可能會產生下列訊息：</span><span class="sxs-lookup"><span data-stu-id="3c98f-144">Some operations might generate the following message:</span></span>

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="3c98f-145">確認指定的叢集端點可以使用且正在接聽。</span><span class="sxs-lookup"><span data-stu-id="3c98f-145">Verify that the specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="3c98f-146">另外確認 Service Fabric Explorer 的 UI 可在該主機和連接埠上使用。</span><span class="sxs-lookup"><span data-stu-id="3c98f-146">Also, verify that the Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="3c98f-147">若要更新端點，請使用 `az sf cluster select`。</span><span class="sxs-lookup"><span data-stu-id="3c98f-147">To update the endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="3c98f-148">詳細記錄</span><span class="sxs-lookup"><span data-stu-id="3c98f-148">Detailed logs</span></span>

<span data-ttu-id="3c98f-149">當您偵錯或回報問題時，詳細記錄通常很有幫助。</span><span class="sxs-lookup"><span data-stu-id="3c98f-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="3c98f-150">Azure CLI 提供全域 `--debug` 旗標，以增加記錄檔的詳細程度。</span><span class="sxs-lookup"><span data-stu-id="3c98f-150">Azure CLI offers a global `--debug` flag that increases the verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="3c98f-151">命令的說明和語法</span><span class="sxs-lookup"><span data-stu-id="3c98f-151">Command help and syntax</span></span>

<span data-ttu-id="3c98f-152">Service Fabric 命令與 Azure CLI 遵循相同的慣例。</span><span class="sxs-lookup"><span data-stu-id="3c98f-152">Service Fabric commands follow the same conventions as Azure CLI.</span></span> <span data-ttu-id="3c98f-153">如需特定命令或一組命令的說明，請使用 `-h` 旗標：</span><span class="sxs-lookup"><span data-stu-id="3c98f-153">For help with a specific command or a group of commands, use the `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="3c98f-154">以下是另一個範例︰</span><span class="sxs-lookup"><span data-stu-id="3c98f-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
