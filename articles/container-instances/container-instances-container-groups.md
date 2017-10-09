---
title: "aaaAzure 容器執行個體容器群組"
description: "了解容器群組在 Azure Container Instances 中的運作方式"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a>Azure Container Instances 中的容器群組

hello Azure 容器執行個體中的最上層資源是容器群組。 本文說明容器群組為何，以及這些群組能夠實現哪些類型的案例。

## <a name="how-a-container-group-works"></a>容器群組的運作方式

容器群組是集合的 hello 取得排程的容器相同的主機電腦和共用的生命週期、 區域網路和存放磁碟區。 它是類似 toohello 概念的*pod*中[Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/)和[DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/)。

hello 下圖顯示包含多個容器的容器群組的範例。

![容器群組範例][container-groups-example]

請注意：

- hello 群組會排定在單一主機上。
- hello 群組會公開單一公用 IP 位址，與一個公開的連接埠。
- hello 群組是由兩個容器所組成。 一個容器會接聽通訊埠 80，而其他 hello 接聽通訊埠 5000。
- hello 群組包含兩個 Azure 檔案共用做為磁碟區掛接，而且每個容器裝載其中一個本機 hello 共用。

### <a name="networking"></a>網路

容器群組會共用 IP 位址以及該 IP 位址上的連接埠命名空間。 tooenable 外部用戶端 tooreach hello 群組內的容器，您必須公開 hello IP 位址和 hello 容器中的 hello 連接埠。 因為 hello 群組內的容器共用連接埠的命名空間，所以不支援連接埠對應。 群組內的容器可以連線到彼此上 hello localhost 透過它們公開的連接埠即使這些連接埠不會公開外部 hello 群組的 IP 位址。

### <a name="storage"></a>儲存體

您可以指定外部磁碟區 toomount 容器群組內。 您可以將這些磁碟區對應到特定群組中的 hello 個別容器內的路徑。

## <a name="common-scenarios"></a>常見案例

多個容器群組是在您想 toodivide 組成的單一功能的工作到容器映像，也可以由不同小組傳遞，有不同的資源需求數少的情況下很有用。 使用範例可能包括：

- 一個應用程式容器和一個記錄容器。 hello 記錄容器會收集 hello 記錄和度量輸出 hello 主應用程式，並將其寫入 toolong 長期的儲存體。
- 一個應用程式和一個監視容器。 定期監視容器 hello 可讓要求 toohello 應用程式 tooensure 它正在執行，並正確回應，並引發警示，如果不是。
- 處理 web 應用程式的容器和容器提取 hello 從原始檔控制的最新內容。

## <a name="next-steps"></a>後續步驟

了解如何太[部署多個容器群組](container-instances-multi-container-group.md)與 Azure Resource Manager 範本。

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png