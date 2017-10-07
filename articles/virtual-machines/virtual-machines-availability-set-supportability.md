---
title: "新增 Azure Vm tooan 現有可用性設定組的 aaaSupportability |Microsoft 文件"
description: "新增 Azure Vm tooan 現有可用性設定組的支援能力。"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a>新增 Azure Vm tooan 現有可用性設定組的支援能力

當您新增新虛擬機器 (Vm) tooan 現有的可用性集合時，您可能偶爾會遇到限制。 hello 下列圖表中，您可以混合的 VM 系列 hello 相同可用性設定組的詳細資料。

以下是 hello 可支援性矩陣 toomix 不同類型的 Vm:

系列與可用性設定組|第二部 VM|具有使用 |Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|第一部 VM|||||||
|具有使用 ||OK|OK|OK|OK|OK|
|Av2||OK|OK|OK|OK|OK|
|D||OK|OK|OK|OK|OK|
|Dv2||OK|OK|OK|OK|OK|
|Dv3||OK|OK|OK|OK|OK|

在相同可用性設定組，因為它們需要特定硬體的 hello 中找不到其他所有數列。
