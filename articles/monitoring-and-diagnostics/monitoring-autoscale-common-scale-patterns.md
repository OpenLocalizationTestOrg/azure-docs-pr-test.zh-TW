---
title: "常見的自動調整規模模式 aaaOverview |Microsoft 文件"
description: "了解一些常見模式 tooauto hello Azure 中調整您的資源。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a>常見的自動調整規模模式概觀
本文將說明一些常見模式 tooscale hello 您在 Azure 中的資源。

只有 tooVirtual 機器規模集 (VMSS)、 雲端服務、 應用程式服務方案和應用程式服務環境，適用於 azure 監視的自動調整規模。 

# <a name="lets-get-started"></a>開始使用

本文假設您已熟悉如何使用自動調整規模。 您可以[取得您的資源已啟動這裡 tooscale][1]。 hello 以下是一些 hello 常見延展模式。

## <a name="scale-based-on-cpu"></a>根據 CPU 調整規模

您具有 Web 應用程式 (/VMSS/雲端服務角色)，而且 

- 您想要 tooscale out/小數位數以根據 CPU。
- 此外，您還想 tooensure 沒有執行個體數目下限。 
- 此外，您想要設定執行個體可調整成最大限制 toohello 數目的 tooensure。

![根據 CPU 調整規模][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a>在工作日與週末以不同方式調整規模

您具有 Web 應用程式 (/VMSS/雲端服務角色)，而且

- 您預設想要 3 個執行個體 (在工作日)
- 您不希望週末的流量，因此想 too1 執行個體關閉 tooscale 週末。

![在工作日與週末以不同方式調整規模][3]

## <a name="scale-differently-during-holidays"></a>在假日期間以不同方式調整規模

您具有 Web 應用程式 (/VMSS/雲端服務角色)，而且 

- 您想要 tooscale 向上/向下預設根據 CPU 使用量
- 不過，在假日旺季期間 （或對您的企業很重要的特定幾天） 時想 toooverride hello 預設值，然後可以利用更多容量。

![在假日期間以不同方式調整規模][4]

## <a name="scale-based-on-custom-metric"></a>根據自訂計量調整規模

您必須在 web 前端和應用程式開發介面層與 hello 後端通訊。 

- 您想根據在 hello 前端的自訂事件 tooscale hello 應用程式開發介面層 (範例： 您想要的 tooscale 您簽出程序根據 hello hello 購物車中的項目數目)

![根據自訂計量調整規模][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png