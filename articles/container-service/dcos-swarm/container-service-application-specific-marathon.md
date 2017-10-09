---
title: "aaaApplication 或特定使用者馬拉松服務 |Microsoft 文件"
description: "建立應用程式或使用者特定的 Marathon 服務"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "容器, Marathon, 微服務, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a>建立應用程式或使用者特定的 Marathon 服務
Azure Container Service 提供了一組主要伺服器，供我們在上面預先設定 Apache Mesos 和 Marathon。 這些可以是使用的 tooorchestrate 上 hello 叢集中，但該應用程式針對此用途的最佳不 toouse hello 主要伺服器。 例如，調整馬拉松 hello 組態需要登入 hello 主要伺服器本身，並進行變更-這鼓勵唯一的方式稍有不同於標準的 hello 和需要 toobe 在意這次的及受管理的主要伺服器獨立。 此外，一個小組所需要的 hello 組態可能不是 hello 為其他小組的最佳組態。

在本文中，我們將說明如何 tooadd 應用程式或使用者特定馬拉松服務。

是免費 tooconfigure tooa 單一使用者或小組，將屬於這個服務，因為它以任何他們想要的方式。 此外，Azure 容器服務可確保 hello 服務仍維持 toorun。 如果 hello 服務失敗時，Azure 容器服務將會重新啟動它為您。 大部分的 hello 時間您將不會注意它有停機時間。

## <a name="prerequisites"></a>必要條件
[部署 Azure 容器服務的執行個體](container-service-deployment.md)與 orchestrator 輸入 DC/OS 和[確定您的用戶端可以連線 tooyour 叢集](../container-service-connect.md)。 此外，請勿 hello 下列步驟。

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a>建立應用程式或使用者特定的 Marathon 服務
開始建立定義 hello 名稱的 toocreate hello 應用程式服務的 JSON 組態檔。 我們在此使用`marathon-alice`為 hello 架構名稱。 將 hello 檔案儲存為類似`marathon-alice.json`:

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

接下來，使用組態檔中所設定的 hello 選項 hello DC/OS CLI tooinstall hello 馬拉松執行個體：

```bash
dcos package install --options=marathon-alice.json marathon
```

您現在應該會看到您`marathon-alice`hello DC/OS UI 的 [服務] 索引標籤中執行的服務。 hello 會在 UI`http://<hostname>/service/marathon-alice/`如果您想 tooaccess 它直接。

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a>設定 hello DC/OS CLI tooaccess hello 服務
您可以選擇性地設定 DC/OS CLI tooaccess 這個新服務所設定的 hello`marathon.url`屬性 toopoint toohello`marathon-alice`執行個體，如下所示：

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

您可以確認哪一個執行個體的 CLI 您正在針對與 hello 的馬拉松`dcos config show`命令。 您可以還原 toousing hello 命令與您主要馬拉松服務`dcos config unset marathon.url`。

