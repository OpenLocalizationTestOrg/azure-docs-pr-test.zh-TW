---
title: "aaaComparing 自訂映像中的和公式 DevTest Labs |Microsoft 文件"
description: "了解 hello 之間差異的自訂映像和公式為 VM 基底，讓您可以決定哪一種最適合您的環境。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a>比較研發/測試實驗室中的自訂映像和公式
[自訂映像](devtest-lab-create-template.md)和[公式](devtest-lab-manage-formulas.md)可以當作[建立新 VM](devtest-lab-add-vm-with-artifacts.md) 的基礎。 不過，hello 金鑰區別自訂映像和公式是自訂映像是只根據 VHD，而公式會根據 VHD 映像的映像*除了*預先設定的 VM 大小，虛擬網路，例如子網路和成品。 這些預先設定的設定會設定使用會覆寫 hello VM 建立時的預設值。 這篇文章會說明一些 hello 優點 （專業人員適用），和缺點 (cons) toousing 自訂映像與使用公式。

## <a name="custom-image-pros-and-cons"></a>自訂映像的優缺點
自訂映像可讓靜態的、 不可變的方式 toocreate Vm 所需的環境。 

**優點**

* 保持不變 hello VM 調整大小之後從 hello 映像，可快速 VM 佈建的自訂映像。 換句話說，任何設定 tooapply hello 自訂映像的影像沒有設定現況。 
* 從單一自訂映像建立的 VM 都相同。

**缺點**

* 如果您需要 tooupdate hello 自訂映像的某些層面，就必須重新建立 hello 映像。  

## <a name="formula-pros-and-cons"></a>公式的優缺點
公式可動態方式 toocreate Vm 所需的 hello/設定。

**優點**

* 可以透過成品 hello 立即擷取 hello 環境中的變更。 例如，如果您想從您的發行管線 hello 最新的位元安裝的 VM，或從您的儲存機制登錄 hello 最新的程式碼，您可以只指定部署 hello 最新的 bits 或登記 hello 搭配 hello 公式中的最新程式碼的成品目標基底映像。 此公式會使用的 toocreate Vm，每當有部署/編列 toohello VM hello 最新的位元/程式碼。 
* 公式可以定義自訂映像無法提供的預設設定 (例如 VM 大小和虛擬網路設定)。 
* 儲存在公式中的 hello 設定為預設值，會顯示，而 hello VM 建立時可以修改。 

**缺點**

* 透過公式建立 VM 所需的時間多於透過自訂映像建立 VM。

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>相關部落格文章
* [自訂映像或公式？](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>後續步驟
- [DevTest Labs 常見問題集](devtest-lab-faq.md)