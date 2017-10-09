---
title: "在 Azure Machine Learning web 服務的 aaaHow tooincrease 並行 |Microsoft 文件"
description: "了解 tooincrease 並行的 Azure Machine Learning web 服務藉由新增其他端點的方式。"
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "azure 機器學習服務, web 服務, 作業化, 調整, 端點, 並行要求"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a>藉由新增其他端點來調整 Azure Machine Learning Web 服務
> [!NOTE]
> 本主題說明的技巧適用 tooa**傳統**機器學習 Web 服務。 
> 
> 

根據預設，每個已發行的 Web 服務是設定的 toosupport 20 的並行要求，而且可以高達 200 的並行要求。 雖然 hello Azure 傳統入口網站提供此值的方式 tooset，Azure Machine Learning 自動 hello 設定 tooprovide hello 最佳效能最佳化您的 web 服務和 hello 入口網站的值會被忽略。 

如果您計劃與更高的負載超過 200 的同時呼叫數目上限值將會支援 toocall hello API，您應該建立多個端點上 hello 相同的 Web 服務。 然後，您就可以將負載隨機分配給所有端點。

hello 調整的 Web 服務是常見的工作。 某些原因 tooscale toosupport 多個並行要求數目 200、 提高可用性，透過多個端點，或為 hello web 服務提供單獨的端點。 您可以透過加入其他端點 hello 提高 hello 小數位數相同的 Web 服務，透過[Azure 傳統入口網站](https://manage.windowsazure.com/)或 hello [Azure Machine Learning Web 服務](https://services.azureml.net/)入口網站。

如需有關新增端點的詳細資訊，請參閱[建立端點](machine-learning-create-endpoint.md)。

請記住，使用高並行計數可能會危害，如果您不呼叫 hello API 跟著率。 您可能會看到偶發的逾時和/或尖峰 hello 延遲時間相對較低負載放在應用程式開發介面，設定為高負載。

hello 通常會使用同步的應用程式開發介面在所需的低延遲的情況。 這裡的延遲表示 hello 時間 hello API toocomplete 一個要求，並不會考量任何網路延遲。 假設您有一個會延遲 50 毫秒的 API。 toofully 取用 hello 與節流層級高的可用容量，以及同時呼叫數目上限 = 20，20 * 1000 這個 API 需要 toocall / 每秒逾 50 = 400。 同時呼叫數目上限為 200 的進一步擴充，可讓您 toocall hello API 4000 時間每秒，假設 50 毫秒延遲。

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
