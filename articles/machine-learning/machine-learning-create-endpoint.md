---
title: "在機器學習中的 aaaCreating Web 服務端點 |Microsoft 文件"
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
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a>建立端點
> [!NOTE]
>  本主題說明的技巧適用 tooa**傳統**機器學習 Web 服務。
> 
> 

當您建立銷售轉寄 tooyour 客戶的 Web 服務時，您必須是哪些 hello Web 服務建立的連結仍 toohello 實驗 tooprovide 定型的模型 tooeach 客戶。 此外，任何更新 toohello 實驗應該套用選擇性 tooan 端點而不覆寫 hello 自訂項目。

tooaccomplish，Azure 機器學習可讓您 toocreate 多個已部署的 Web 服務的端點。 Hello Web 服務中的每個端點獨立定址，節流處理，並管理。 每個端點都是唯一的 URL 和授權的索引鍵，您可以將發佈 tooyour 客戶。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a>加入端點 tooa Web 服務
有三種方式 tooadd 端點 tooa Web 服務。

* 以程式設計方式
* 透過 hello Azure 機器學習 Web 服務入口網站
* 雖然 hello Azure 傳統入口網站

Hello 端點建立之後，您可以使用它，透過同步應用程式開發介面，批次應用程式開發介面，和 excel 工作表。 除了透過此 UI tooadding 端點，您也可以使用 hello 端點管理 Api tooprogrammatically 加入端點。

> [!NOTE]
> 如果您已經加入其他端點 toohello Web 服務，您無法刪除 hello 預設端點。
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>以程式設計方式新增端點
您可以加入端點 tooyour Web 服務以程式設計方式使用 hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs)範例程式碼。

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a>加入使用 hello Azure 機器學習 Web 服務入口網站的端點
1. 在機器學習 Studio 中，在 hello 左側瀏覽資料行中，按一下 Web 服務。
2. 在 hello hello Web 服務儀表板底部，按一下 **管理端點**。 hello Azure 機器學習 Web 服務入口網站開啟 toohello hello Web 服務端點 頁面。
3. 按一下 [新增] 。
4. 輸入的名稱和描述 hello 新端點。 端點名稱長度不可超過 24 個字元，而且必須由小寫字母或數字組成。 選取 hello 記錄層級，以及是否啟用範例資料。 如需有關記錄的詳細資訊，請參閱[為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a>加入使用 hello Azure 傳統入口網站的端點
1. 登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com)，按一下  **Machine Learning** hello 左側資料行中。 按一下 hello 工作區，其中包含您感興趣的 hello Web 服務。
   
    ![瀏覽 tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. 按一下 [Web 服務] 。
   
    ![瀏覽 tooWeb 服務](./media/machine-learning-create-endpoint/figure-2.png)
3. 按一下您想要在 toosee hello 可用的端點清單中的 hello Web 服務。
   
    ![瀏覽 tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. 在 hello hello 頁面底部，按一下**加入端點**。 輸入名稱和描述，請確定沒有其他端點與此 Web 服務中名稱相同的 hello。 保留 hello 節流層級以預設值，除非您有特殊需求。 toolearn 深入了解節流，請參閱[調整應用程式開發介面端點](machine-learning-scaling-webservice.md)。
   
    ![建立端點](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>後續步驟
[如何在 Azure 機器學習 Web 服務 tooconsume](machine-learning-consume-web-services.md)。

