---
title: "aaaHow tooscale Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "本教學課程涵蓋如何 tooscale Azure 時間數列 Insights 環境"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a>如何 tooscale 時間數列 Insights 環境

本教學課程涵蓋如何 tooscale 時間數列 Insights 環境。

> [!NOTE]
> 若 SKU 類型不同則無法進行相應增加。 S1 SKU 的環境不能轉換成 S2 環境。

## <a name="s1-sku-ingress-rates-and-capacities"></a>S1 SKU 輸入速率和容量

| S1 SKU 容量 | 輸入速率 | 儲存體容量上限
| --- | --- | --- |
| 1 | 1 GB (1 百萬個事件) | 一個月 30 GB (3 千萬個事件) |
| 10 | 10 GB (1 千萬個事件) | 一個月 300 GB (3 億個事件) |

## <a name="s2-sku-ingress-rates-and-capacities"></a>S2 SKU 輸入速率和容量

| S2 SKU 容量 | 輸入速率 | 儲存體容量上限
| --- | --- | --- |
| 1 | 10 GB (1 千萬個事件) | 一個月 300 GB (3 億個事件) |
| 10 | 100 GB (1 億個事件) | 一個月 3 TB (30 億個事件) |

容量是以線性方式擴充或減少，因此容量 2 的 S1 SKU 支援的輸入速率為一天 2 GB (2 百萬) 的事件，和 一個月 60 GB (6 千萬個事件)。

## <a name="changing-hello-capacity-of-your-environment"></a>變更環境的 hello 容量

1. 在 hello Azure 入口網站，選取 hello 環境的容量想 toochange。
1. 在 [設定] 下方按一下 [設定]。
1. 使用 hello 容量滑桿 tooselect hello 產能符合您的輸入速率的 hello 需求和儲存體容量。

## <a name="next-steps"></a>後續步驟

* 確認 hello 新容量足夠 tooprevent 節流。 如需詳細資訊，請參閱 hello*您的環境可能會節流*區段[這裡](time-series-insights-diagnose-and-solve-problems.md)。
