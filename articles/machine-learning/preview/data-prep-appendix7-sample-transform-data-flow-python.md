---
title: "可用於 Azure Machine Learning 資料準備之轉換資料流程轉換的範例 | Microsoft Docs"
description: "本文件提供可用於 Azure Machine Learning 資料準備之轉換資料流程轉換的一組範例"
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
ms.openlocfilehash: 4a716c1934258e687eb48ecb4077c6be7b269c1f
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/04/2018
---
# <a name="sample-of-custom-data-flow-transforms-python"></a>自訂資料流程轉換的範例 (Python) 
功能表中的轉換名稱是**轉換資料流程 (指令碼)**。 閱讀本附錄之前，請先參閱 [Python 擴充性概觀](data-prep-python-extensibility-overview.md)。

## <a name="transform-frame"></a>轉換框架
### <a name="create-a-new-column-dynamically"></a>以動態方式建立新的資料行 
以動態方式建立資料行 (**city2**)，並且將現有城市資料行的多個不同版本 San Francisco 調解成一個。
```python
    df.loc[(df['city'] == 'San Francisco') | (df['city'] == 'SF') | (df['city'] == 'S.F.') | (df['city'] == 'SAN FRANCISCO'), 'city2'] = 'San Francisco'
```

### <a name="add-new-aggregates"></a>新增新的彙總
建立新的框架，具有針對分數資料行計算的第一個和最後一個彙總。 這些彙總是依據 **risk_category** 資料行來分組。
```python
    df = df.groupby(['risk_category'])['Score'].agg(['first','last'])
```
### <a name="winsorize-a-column"></a>對資料行進行極端值調整 
重新編寫資料以符合在資料行中減少極端值的公式。
```python
    import scipy.stats as stats
    df['Last Order'] = stats.mstats.winsorize(df['Last Order'].values, limits=0.4)
```

## <a name="transform-data-flow"></a>轉換資料流程
### <a name="fill-down"></a>向下填滿 
向下填滿需要兩個轉換。 其採用如下所示的資料：


|State         |City       |
|--------------|-----------|
|Washington    |Redmond    |
|              |Bellevue   |
|              |Issaquah   |
|              |Seattle    |
|California    |洛杉磯|
|              |San Diego  |
|              |San Jose   |
|Texas         |達拉斯     |
|              |San Antonio|
|              |Houston    |

首先，建立包含下列程式碼的「新增資料行 (指令碼)」轉換：
```python
    row['State'] if len(row['State']) > 0 else None
```
現在建立包含下列程式碼的「轉換資料流程 (指令碼)」轉換：
```python
    df = df.fillna( method='pad')
```

資料現在如下所示：

|State         |newState         |City       |
|--------------|--------------|-----------|
|Washington    |Washington    |Redmond    |
|              |Washington    |Bellevue   |
|              |Washington    |Issaquah   |
|              |Washington    |Seattle    |
|California    |California    |洛杉磯|
|              |California    |San Diego  |
|              |California    |San Jose   |
|Texas         |Texas         |達拉斯     |
|              |Texas         |San Antonio|
|              |Texas         |Houston    |


### <a name="min-max-normalization"></a>最小值最大值正規化
```python
    df["NewCol"] = (df["Col1"]-df["Col1"].mean())/df["Col1"].std()
```