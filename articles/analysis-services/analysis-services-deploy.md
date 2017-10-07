---
title: "使用 SSDT aaaDeploy tooAzure Analysis Services |Microsoft 文件"
description: "了解表格式模型 tooan toodeploy Azure Analysis Services 如何使用 SSDT 的伺服器。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a>從 SSDT 部署模型
您的 Azure 訂用帳戶中建立的伺服器之後，您已準備好 toodeploy 表格式模型資料庫 tooit。 您可以使用 SQL Server Data Tools (SSDT) toobuild 並部署您在處理表格式模型專案。 

## <a name="prerequisites"></a>必要條件
tooget 開始，您需要：

* Azure 中的 **Analysis Services 伺服器**。 詳細資訊，請參閱 toolearn[建立 Azure Analysis Services 伺服器](analysis-services-create-server.md)。
* **表格式模型專案**SSDT 或現有的表格式模型在 hello 1200 或更高的相容性層級中。 未曾建立過？ 再試一次 hello [Adventure Works 網際網路銷售的表格式模型教學課程](https://msdn.microsoft.com/library/hh231691.aspx)。
* **在內部部署閘道**-如果一或多個資料來源位於內部部署組織的網路中，您需要 tooinstall[在內部部署資料閘道](analysis-services-gateway.md)。 您的伺服器 hello 雲端連線 tooyour 在內部部署資料來源 tooprocess 和重新整理模型中的資料 hello hello 閘道是必要的。

> [!TIP]
> 在部署之前，請確定您可以處理 hello 資料在資料表中。 在 SSDT 中，按一下 [模型]  >  [程序]  >  **Process All** (全部處理)。 如果處理失敗，您就無法部署成功。
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a>toodeploy 從 SSDT 的表格式模型

1. 在部署之前，您會需要 tooget hello 伺服器名稱。 在**Azure 入口網站**> 伺服器 >**概觀** > **伺服器名稱**，複製 hello 伺服器名稱。
   
    ![在 Azure 中取得伺服器名稱](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. 在 SSDT 中 >**方案總管 中**，以滑鼠右鍵按一下 hello 專案 >**屬性**。 接著在**部署** > **伺服器**貼上 hello 伺服器名稱。   
   
    ![將伺服器名稱貼到部署伺服器屬性](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. 在 [方案總管] 中，以滑鼠右鍵按一下 [屬性]，然後按一下 [部署]。 您可能會提示的 toosign tooAzure 中。
   
    ![部署 tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    部署狀態會出現在這兩個 hello 輸出 視窗和部署。
   
    ![部署狀態](./media/analysis-services-deploy/aas-deploy-status.png)

這就是沒有 tooit ！


## <a name="troubleshooting"></a>疑難排解
如果部署失敗部署中繼資料時，它可能是因為 SSDT 無法 tooyour 伺服器連接。 請確定您可以使用 SSMS 的 tooyour 伺服器連接。 請確定 hello hello 專案的 [部署伺服器] 屬性正確。

如果部署失敗的資料表上，它可能是因為您的伺服器無法連線 tooa 資料來源。 如果您的資料來源是內部部署組織的網路中，是確定 tooinstall[在內部部署資料閘道](analysis-services-gateway.md)。

## <a name="next-steps"></a>後續步驟
有您的表格式模型部署的 tooyour 伺服器之後，您準備好 tooconnect tooit。 您可以[使用 SSMS 連接 tooit](analysis-services-manage.md) toomanage 它。 而且，您可以[連接使用用戶端工具 tooit](analysis-services-connect.md)喜歡 Power BI、 Power BI Desktop 或 Excel 及建立報表的開始。

