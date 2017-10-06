---
title: "aaaConnect tooAzure Analysis Services 與 Excel |Microsoft 文件"
description: "了解 tooconnect tooan Azure Analysis Services 如何使用 Excel 的伺服器。"
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
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a>使用 Excel 進行連接

在 Azure 中，建立伺服器並部署表格式模型 tooit 之後，您正在準備 tooconnect 並開始探索資料。


## <a name="connect-in-excel"></a>在 Excel 中連線

在 Excel 中的 tooa 伺服器連接支援 Excel 2016 中使用 取得資料。 不支援使用 Power Pivot 中的 hello 匯入資料表精靈 連接。 

**在 Excel 2016 tooconnect**

1. 在 Excel 2016 中，在 hello**資料**功能區中，按一下 **取得外部資料** > **從其他來源** > **從 Analysis Services**.

2. 在 [hello 資料連線精靈] 中**伺服器名稱**，輸入 hello 伺服器名稱，包括通訊協定和 URI。 然後，在**登入認證**，選取**下列使用者名稱和密碼使用 hello**，然後輸入 hello 組織的使用者名稱，例如nancy@adventureworks.com，和密碼。

    ![從 Excel 登入來進行連接](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. 在**選取資料庫和資料表**hello 資料庫和模型或檢視方塊，選取，然後按一下**完成**。
   
    ![從 Excel 選取模型來進行連接](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a>另請參閱
[用戶端程式庫](analysis-services-data-providers.md)   
[管理您的伺服器](analysis-services-manage.md)     


