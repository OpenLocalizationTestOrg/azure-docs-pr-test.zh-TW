---
title: "aaaConnect tooAzure Analysis Services 與 Power BI |Microsoft 文件"
description: "了解 tooconnect tooan Azure Analysis Services 如何使用 Power BI 的伺服器。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a>使用 Power BI 進行連接

在 Azure 中，建立伺服器並部署表格式模型 tooit 之後，您的組織中的使用者會準備 tooconnect，並開始瀏覽資料。 

> [!TIP]
> 要確定 toouse hello 最新版本的[Power BI Desktop](https://powerbi.microsoft.com/desktop/)。
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a>在 Power BI Desktop 中連線

1. 在 Power BI Desktop 中，按一下 [取得資料] > [Azure] > [Azure Analysis Services 資料庫]。

2. 在**伺服器**，輸入 hello 伺服器名稱。 
    
    是確定 tooinclude hello 完整 URL。 例如 asazure://westcentralus.asazure.windows.net/advworks。

3. 在**資料庫**，如果您知道 hello hello 表格式模型資料庫或要 tooconnect 若要貼至此處的檢視方塊名稱。 否則，您可以將此欄位保留空白，然後稍後選取資料庫或檢視方塊。

4. 保留預設值，hello**即時連接**選項，然後按**連接**。 

5. 如果出現提示，請輸入您的登入認證。 

6. 在**導覽**，展開 hello 伺服器，然後選取 hello 模型或您想要 tooconnect 至，然後按一下 檢視方塊**連接**。 按一下模型或檢視方塊 tooshow 適用於該檢視的所有 hello 物件。

    報表檢視中的空白報表與 Power BI Desktop 中開啟 hello 模型。 hello 欄位清單會顯示所有非隱藏的模型物件。 連接狀態會顯示在 hello 右下角。

## <a name="connect-in-power-bi-service"></a>在 Power BI Desktop 中連線 (服務)

1. 建立您的伺服器具有即時連接 tooyour 模型的 Power BI Desktop 檔案。
2. 在 [Power BI](https://powerbi.microsoft.com) 中，按一下 [取得資料]  >  [檔案]。 找到並選取您的檔案。



## <a name="see-also"></a>另請參閱
[連接 tooAzure Analysis Services](analysis-services-connect.md)   
[用戶端程式庫](analysis-services-data-providers.md)

