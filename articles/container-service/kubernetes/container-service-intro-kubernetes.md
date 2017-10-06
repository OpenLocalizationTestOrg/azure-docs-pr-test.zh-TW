---
title: "aaaIntroduction tooAzure Kubernetes 的容器服務 |Microsoft 文件"
description: "Kubernetes azure 容器服務便可簡單 toodeploy 並管理容器應用程式在 Azure 上。"
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, 容器, 微服務, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a>簡介 tooAzure Kubernetes 的容器服務
使得簡單 toocreate Kubernetes azure 容器服務、 設定和管理所預先設定的 toorun 容器化應用程式的虛擬機器的叢集。 這可讓您 toouse 您現有的技術，或運用社群專業知識，toodeploy 大量且不斷主體和管理容器應用程式在 Microsoft Azure 上。

藉由使用 Azure 容器服務，您可以利用 hello 企業級功能的 Azure，同時仍維持 Kubernetes 透過應用程式可攜性和 hello Docker 映像格式。

## <a name="using-azure-container-service-for-kubernetes"></a>使用 Azure Container Service for Kubernetes
我們使用 Azure 容器服務的目標是使用開放原始碼工具和技術，現在都可以在我們的客戶之間的熱門 tooprovide 容器主機環境。 toothis 結束時，我們展現 hello 標準 Kubernetes API 端點。 藉由使用這些標準端點，您可以利用能夠進行交談 tooa Kubernetes 叢集的任何軟體。 例如，您可能會選擇 [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)、[helm](https://helm.sh/) 或 [draft](https://github.com/Azure/draft)。

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>使用 Azure Container Service 建立 Kubernetes 叢集
使用 Azure 的容器服務 toobegin 部署 Azure 容器服務叢集以 hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md)或透過 hello 入口網站 (搜尋 hello Marketplace 的**Azure 容器服務**)。 如果您需要更充分掌控 hello Azure Resource Manager 範本的進階的使用者，您可以使用 hello 開放原始碼[acs 引擎](https://github.com/Azure/acs-engine)專案 toobuild 您自己自訂的 Kubernetes 叢集，並將其部署透過 hello `az` CLI。

### <a name="using-kubernetes"></a>使用 Kubernetes
Kubernetes 能自動化部署、調整和管理容器化應用程式。 它包含一組豐富的功能，包括︰
* 自動 binpacking
* 自我修復
* 水平調整
* 服務探索和負載平衡
* 自動化推出和復原
* 祕密和組態管理
* 儲存體協調流程
* 批次執行

透過 Container Service 部署的 Kubernetes 架構圖：

![Azure 容器服務設定 toouse Kubernetes。](media/acs-intro/kubernetes.png)

## <a name="videos"></a>影片

Azure Container Service 中的 Kubernetes 支援 (Azure Friday，2017 年 1 月)：

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

用於在 Kubernetes 開發及部署應用程式的工具 (Azure OpenDev，2017 年 6 月)：

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>後續步驟

瀏覽 hello [Kubernetes 快速入門](container-service-kubernetes-walkthrough.md)toobegin 今天瀏覽 Azure 容器服務。
