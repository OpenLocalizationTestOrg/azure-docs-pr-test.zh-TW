---
title: "aaaAzure 容器登錄儲存機制 |Microsoft 文件"
description: "如何針對 Docker 映像 toouse Azure 容器登錄中儲存機制"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Azure 容器登錄存放庫

Azure Container Registry 與許多服務和 Orchestrator 相容。 toomake 它更容易 tootrack hello 來源服務和代理程式從中使用 ACR，我們已開始使用 hello Docker.config 檔案中的 hello Docker 標頭欄位。



## <a name="viewing-repositories-in-hello-portal"></a>在 hello 入口網站中檢視儲存機制

hello ACR 標頭，請遵循 hello 格式：
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* 雲端：Azure、Azure Stack 或是其他政府或國家/地區特定的 Azure 雲端。 雖然目前不支援 Azure Stack 和政府雲端，此參數未來可允許支援。
* 服務： hello 服務名稱。
* Optionalservicename： 服務與子服務或 toospecify SKU 選擇性參數 (例如： web 應用程式會與 Azure/應用程式層服務/web 層應用程式的對應)。

協力廠商服務和 orchestrators 是鼓勵的 toouse 特定標頭值 toohelp 與我們的遙測。 使用者也可以修改 hello 依需要傳遞 toohello 標頭的值。

hello 我們想要的 ACR 夥伴 toouse toopopulate hello 「 X-中繼-來源-用戶端 」 欄位的值如下：

| 服務名稱              | 頁首                                |
| ------------------------- | ------------------------------------- |
| Azure Container Service   | azure/compute/azure-container-service |
| App Service - Web Apps    | azure/app-service/web-apps            |
| App Service - Logic Apps  | azure/app-service/logic-apps          |
| 批次                     | azure/compute/batch                   |
| 雲端主控台             | azure/cloud-console                   |
| Functions                 | azure/compute/functions               |
| 物聯網 - 中樞  | azure/iot/hub                         |
| HDInsight                 | azure/data/hdinsight                  |
| Jenkins                   | azure/jenkins                         |
| 機器學習服務          | azure/data/machile-learning           |
| Service Fabric            | azure/compute/service-fabric          |
| VSTS                      | azure/vsts                            |


## <a name="next-steps"></a>後續步驟
[深入了解登錄和 orchestrators hello 支援服務](container-registry-intro.md)
