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
# <a name="azure-service-fabric-command-line"></a>Azure Service Fabric 命令列

hello Azure Service Fabric CLI (sfctl) 是命令列公用程式互動，及管理 Azure Service Fabric 實體。 Sfctl 可以搭配 Windows 或 Linux 叢集使用。 Sfctl 可在支援 python 的任何平台上執行。

## <a name="prerequisites"></a>必要條件

先前 tooinstallation，請確定您的環境具有 python 和安裝的 pip。 如需詳細資訊，看看 hello [pip 快速入門文件](https://pip.pypa.io/en/latest/quickstart/)，和官方[python 安裝文件集](https://wiki.python.org/moin/BeginnersGuide/Download)。

雖然這兩個 python 2.7 和 3.6 受到支援，但建議 toouse python 3.6。

## <a name="install"></a>Install

hello Azure Service Fabric CLI (sfctl) 會封裝成 python 封裝。 tooinstall hello 最新版本執行：

```bash
pip install sfctl
```

安裝之後，執行`sfctl -h`tooget 可用命令的資訊。

## <a name="cli-syntax"></a>CLI 語法

命令前面一律會加上 `sfctl`。 如需有關所有命令的一般資訊，請使用 `sfctl -h`。 如需單一命令的說明，請使用 `sfctl <command> -h`。

命令後續可重複結構，與 hello 目標的 hello 命令前面的動作或 hello 動詞命令：

```azurecli
sfctl <object> <action>
```

在此範例中， `<object>` hello 的目標`<action>`。

## <a name="select-a-cluster"></a>選取叢集

在執行任何作業之前，您必須選取要叢集 tooconnect。 比方說，執行下列 tooselect hello 和連接 hello 名稱 toohello 叢集`testcluster.com`。

> [!WARNING]
> 請勿於生產環境中使用不安全的 Service Fabric 叢集。

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

hello 叢集端點都必須加`http`或`https`。 它必須包括 hello hello HTTP 閘道的連接埠。 hello 連接埠和位址都 hello 與 hello Service Fabric 總管 URL 相同。

對於使用憑證保護的叢集，您可以指定 PEM 編碼的憑證。 hello 憑證可以指定為單一檔案或憑證和金鑰組。

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

如需詳細資訊，請參閱[連接 tooa 安全 Azure Service Fabric 叢集](service-fabric-connect-to-secure-cluster.md)。

## <a name="basic-operations"></a>基本作業

叢集連線資訊會跨多個 sfctl 工作階段保存。 選取 Service Fabric 叢集之後，您可以在 hello 叢集上執行任何 Service Fabric 命令。

比方說，tooget hello Service Fabric 叢集健全狀況狀態，會使用下列命令的 hello:

```azurecli
sfctl cluster health
```

hello 命令會產生下列輸出的 hello:

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

用於解決一般問題的某些建議和秘訣。

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>將憑證從 PFX tooPEM 格式轉換

服務網狀架構 CLI hello 支援 PEM （副檔名為.pem） 檔案和用戶端憑證。 如果您從 Windows 使用 PFX 檔案，您必須將這些憑證 tooPEM 格式轉換。 tooconvert PFX 檔案 tooa PEM 檔案，請使用下列命令：

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

如需詳細資訊，請參閱 hello [OpenSSL 文件](https://www.openssl.org/docs/)。

### <a name="connection-issues"></a>連接問題

某些作業可能會產生下列訊息的 hello:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

請確認該 hello 可讓您指定叢集端點可供使用和接聽。 此外，請確認該 hello Service Fabric 總管 UI 位於的主機和連接埠。 tooupdate hello 端點，使用`sfctl cluster select`。

### <a name="detailed-logs"></a>詳細記錄

當您偵錯或回報問題時，詳細記錄通常很有幫助。 沒有全域`--debug`旗標，會增加 hello 的記錄檔的詳細資訊。

### <a name="command-help-and-syntax"></a>命令的說明和語法

與特定命令或一組命令的說明，請使用 hello`-h`旗標：

```azurecli
sfctl application -h
```

另一個範例：

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a>後續步驟

* [部署應用程式以 hello Azure Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md)
* [在 Linux 上開始使用 Service Fabric](service-fabric-get-started-linux.md)
