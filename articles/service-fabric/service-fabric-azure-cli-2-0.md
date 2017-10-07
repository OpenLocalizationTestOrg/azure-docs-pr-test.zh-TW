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
# <a name="azure-service-fabric-and-azure-cli-20"></a>Azure Service Fabric 和 Azure CLI 2.0

hello Azure 命令列工具 (Azure CLI) 2.0 版包含命令 toohelp 您管理 Azure Service Fabric 叢集。 了解 tooget 如何開始使用 Azure CLI 和服務網狀架構。

## <a name="install-azure-cli-20"></a>安裝 Azure CLI 2.0

您可以使用 Azure CLI 2.0 命令 toointeract 與和管理 Service Fabric 叢集。 tooget hello 最新版本的 Azure CLI，後續 hello [Azure CLI 2.0 標準安裝程序](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。

如需詳細資訊，請參閱 hello [Azure CLI 2.0 概觀](https://docs.microsoft.com/en-us/cli/azure/overview)。

## <a name="azure-cli-syntax"></a>Azure CLI 語法

在 Azure CLI 中，所有 Service Fabric 命令前面都會加上 `az sf`。 您可以使用 hello 命令的相關的一般資訊，請使用`az sf -h`。 如需單一命令的說明，請使用 `az sf <command> -h`。

Azure CLI 中的 Service Fabric 命令會遵循此命名模式：

```azurecli
az sf <object> <action>
```

`<object>`是 hello 目標`<action>`。

## <a name="select-a-cluster"></a>選取叢集

在執行任何作業之前，您必須選取要叢集 tooconnect。 如需範例，請參閱下列程式碼的 hello。 hello 程式碼連接 tooan 不安全的叢集。

> [!WARNING]
> 請勿於生產環境中使用不安全的 Service Fabric 叢集。

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

hello 叢集端點都必須加`http`或`https`。 它必須包括 hello hello HTTP 閘道的連接埠。 hello 連接埠和位址都 hello 與 hello Service Fabric 總管 URL 相同。

對於使用憑證保護的叢集，您可以使用未加密的 .pem 檔案或 .crt 和 .key 檔案。 例如：

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

如需詳細資訊，請參閱[連接 tooa 安全 Azure Service Fabric 叢集](service-fabric-connect-to-secure-cluster.md)。

> [!NOTE]
> hello`select`之前它會傳回命令不會處理任何要求。 您所指定的叢集是否正確，tooverify 使用類似的命令`az sf cluster health`。 請確認 hello 命令不會傳回任何錯誤。

## <a name="basic-operations"></a>基本作業

叢集連線資訊會跨多個 Azure CLI 工作階段保存。 選取 Service Fabric 叢集之後，您可以在 hello 叢集上執行任何 Service Fabric 命令。

比方說，tooget hello Service Fabric 叢集健全狀況狀態，會使用下列命令的 hello:

```azurecli
az sf cluster health
```

hello 命令會產生 hello 下列輸出 （假設 hello Azure CLI 組態中所指定 JSON 輸出）：

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

## <a name="tips-and-troubleshooting"></a>秘訣與疑難排解

您可能會發現您在使用 Azure CLI Service Fabric 命令時遇到問題時，下列資訊很有幫助的 hello。

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>將憑證從 PFX tooPEM 格式轉換

Azure CLI 支援以 PEM (.pem 副檔名) 檔案作為用戶端憑證。 如果您從 Windows 使用 PFX 檔案，您必須將這些憑證 tooPEM 格式轉換。 tooconvert PFX 檔案 tooa PEM 檔案，請使用下列命令的 hello:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

如需詳細資訊，請參閱 hello [OpenSSL 文件](https://www.openssl.org/docs/)。

### <a name="connection-issues"></a>連接問題

某些作業可能會產生下列訊息的 hello:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

請確認該 hello 可讓您指定叢集端點可供使用和接聽。 此外，請確認該 hello Service Fabric 總管 UI 位於的主機和連接埠。 tooupdate hello 端點，使用`az sf cluster select`。

### <a name="detailed-logs"></a>詳細記錄

當您偵錯或回報問題時，詳細記錄通常很有幫助。 Azure CLI 提供全域`--debug`旗標，會增加 hello 的記錄檔的詳細資訊。

### <a name="command-help-and-syntax"></a>命令的說明和語法

Service Fabric 命令後續 hello Azure CLI 為相同的慣例。 與特定命令或一組命令的說明，請使用 hello`-h`旗標：

```azurecli
az sf application -h
```

以下是另一個範例︰

```azurecli
az sf application create -h
```
