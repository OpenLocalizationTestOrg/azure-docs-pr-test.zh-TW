---
title: "在 Machine Learning 中建立 Web 服務端點 | Microsoft Docs"
description: "在 Azure Machine Learning 中建立 Web 服務端點"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 9f83ffc9cf7dbe37c1ce9980fd7f5b9133fe78f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="creating-endpoints"></a>建立端點
> [!NOTE]
>  此主題描述適用於**傳統** Machine Learning Web 服務的技巧。
> 
> 

當您建立會進而銷售給客戶的 Web 服務時，必須為每位客戶提供仍連結至建立 Web 服務之實驗的定型模型。 此外，實驗的任何更新都應可以選擇性地套用到整個端點，而不會覆寫自訂項目。

為了達到這個目的，Azure Machine Learning 允許您為已部署的 Web 服務建立多個端點。 Web 服務的每個端點都是個別定址、節流以及管理。 每個端點是一個唯一 URL 和授權金鑰，您可散發給您的客戶。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a>將端點新增至 Web 服務
有三種方式可在 Web 服務中新增端點。

* 以程式設計方式
* 透過 Azure Machine Learning Web 服務入口網站
* 透過 Azure 傳統入口網站

建立端點之後，您就可以透過同步 API、批次 API 以及 Excel 工作表來取用該端點。 除了透過此 UI 新增端點之外，您也可以使用端點管理 API，以程式設計方式加入端點。

> [!NOTE]
> 如果您已在 Web 服務中新增額外的端點，就無法刪除預設端點。
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>以程式設計方式新增端點
您可以使用 [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) 範例程式碼，以程式設計方式將端點新增至您的 Web 服務。

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a>使用 Azure Machine Learning Web 服務入口網站新增端點
1. 在 Machine Learning Studio 中，按一下左側的 [Web 服務]。
2. 在 Web 服務儀表板底部，按一下 [管理端點]。 Azure Machine Learning Web 服務 入口網站會開啟 Web 服務的端點頁面。
3. 按一下 [新增] 。
4. 輸入新端點的名稱和描述。 端點名稱長度不可超過 24 個字元，而且必須由小寫字母或數字組成。 選取記錄層級，以及是否啟用範例資料。 如需有關記錄的詳細資訊，請參閱[為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。

## <a name="adding-an-endpoint-using-the-azure-classic-portal"></a>使用 Azure 傳統入口網站新增端點
1. 登入 [Azure 傳統入口網站](http://manage.windowsazure.com)，按一下左欄中的 [Machine Learning]。 按一下包含您感興趣之 Web 服務的工作區。
   
    ![瀏覽到工作區](./media/machine-learning-create-endpoint/figure-1.png)
2. 按一下 [Web 服務] 。
   
    ![瀏覽到 Web 服務](./media/machine-learning-create-endpoint/figure-2.png)
3. 按一下您感興趣的 Web 服務，以查看可用端點的清單。
   
    ![瀏覽到端點](./media/machine-learning-create-endpoint/figure-3.png)
4. 按一下頁面底部的 [新增端點] 。 輸入名稱和描述，確定此 Web 服務中沒有名稱相同的其他端點。 除非您有特殊需求，否則請保留節流層級的預設值。 若要深入了解節流，請參閱[調整 API 端點](machine-learning-scaling-webservice.md)。
   
    ![建立端點](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>後續步驟
[如何使用 Azure Machine Learning Web 服務](machine-learning-consume-web-services.md)。

