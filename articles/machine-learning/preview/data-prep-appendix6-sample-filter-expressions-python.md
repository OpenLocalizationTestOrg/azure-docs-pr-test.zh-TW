---
title: "可用於 Azure Machine Learning 資料準備之篩選條件運算式的範例 | Microsoft Docs"
description: "本文件提供可用於 Azure Machine Learning 資料準備之篩選條件運算式的一組範例"
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.custom: 
ms.devlang: 
ms.topic: article
ms.date: 09/11/2017
ms.openlocfilehash: ae70f5981c7ca533740968e0eea1b0b83df414fa
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2017
---
# <a name="sample-of-filter-expressions-python"></a>篩選條件運算式的範例 (Python) 
閱讀本附錄之前，請先參閱 [Python 擴充性概觀](data-prep-python-extensibility-overview.md)。

## <a name="filter-with-equivalence-test"></a>等價測試篩選
僅篩選 (數值) Col2 值大於 4 的資料列。 

```python
    row["Col2"] > 4
```

## <a name="filter-with-multiple-columns"></a>多個資料行篩選 
僅篩選 Col1 包含 **Good** 值且 Col2 包含 (數值) 值 1 的資料列。 
```python
    row["Col1"] == 'Good' and row["Col2"] == 1
```

## <a name="test-filter-against-null"></a>對應 Null 測試篩選
僅篩選 Col1 具有 Null 值的資料列。 
```python
    pd.isnull(row["Col1"])
```
