---
title: "aaaAzure 容器執行個體概觀 |Azure 文件"
description: "了解 Azure Container Instances"
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
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a>Azure Container Instances

容器快速成為 hello 慣用方式 toopackage、 部署及管理雲端應用程式。 Azure 容器執行個體提供最快的 hello 和最簡單方式 toorun 容器在 Azure 中，而不需要 tooprovision 任何虛擬機器，而不需要 tooadopt 較高層級的服務。 

對於可在隔離容器中運作的任何情節，包括簡單的應用程式、工作自動化及建置工作，Azure Container Instances 是很棒的解決方案。 您需要在此完整容器協調流程，包括跨多個容器、 自動縮放功能，以及協調應用程式升級，服務探索的案例中，我們建議 hello [Azure 容器服務](https://docs.microsoft.com/azure/container-service/)。

## <a name="fast-startup-times"></a>快速啟動時間

容器提供比虛擬機器更多的啟動優點。 Azure 容器執行個體中，您可以在 Azure 中啟動容器，以秒為單位，而不 hello 需要 tooprovision 並管理 Vm。

## <a name="hypervisor-level-security"></a>Hypervisor 等級安全性

在過去，雖然容器提供應用程式相依性隔離和資源控管，但並沒有足夠的能力防範惡意的多租用戶使用方式。 Azure Container Instances 可以將您的應用程式隔離在容器中，就像在 VM 中一樣。

## <a name="custom-sizes"></a>自訂大小

容器是通常最佳化的 toorun 只是單一的應用程式，而 hello 的特定需求，這些應用程式可以有明顯的差異。 Azure Container Instances 可讓您要求剛好符合所需的 CPU 核心和記憶體數量。 您必須支付根據要求什麼方法，計費由 hello 秒，讓您精密地可以將您的需求為基礎的費用。

## <a name="public-ip-connectivity"></a>公用 IP 連線能力

Azure 容器執行個體中，您可以將您的容器公開直接 toohello 網際網路的公用 IP 位址。 在未來的 hello，我們將會展開我們網路功能 tooinclude 與虛擬網路整合、 負載平衡器、 與 hello Azure 網路基礎結構的其他核心部分。

## <a name="persistent-storage"></a>永續性儲存體

tooretrieve 和保存 Azure 容器執行個體的狀態，因此我們提供的 Azure 直接掛接檔案共用。

## <a name="linux-and-windows-containers"></a>Linux 和 Windows 容器

Azure 容器執行個體中，您可以排程 Windows 和 Linux 容器與 hello 相同的 API。 只會表示都有相同基底 OS 類型 hello 和其他項目。

## <a name="co-scheduled-groups"></a>共同排程的群組

Azure Container Instances 支援排程多個共用主機、區域網路、儲存體和生命週期的容器群組。 這可讓您 toocombine 主應用程式與其他人扮演支援的角色，例如記錄。

## <a name="next-steps"></a>後續步驟

嘗試部署與單一命令，使用容器 tooAzure 我們[快速入門指南](container-instances-quickstart.md)。
