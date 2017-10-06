---
title: "aaaHow toodeploy Web 服務 toomultiple 區域 |Microsoft 文件"
description: "步驟 toodeploy （複製） 新的 Web 服務 tooother 區域。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a>如何 toodeploy Web 服務 toomultiple 區域
hello 新 Azure Web 服務可讓您 tooeasily 部署 web 服務 toomultiple 區域，而不需要多個訂用帳戶或工作區。 

定價是區域特定，因此您必須定義每個區域中，您將部署 hello web 服務的計費方案。

## <a name="toocreate-a-plan-in-another-region"></a>toocreate 另一個區域中的計畫
1. 登入 [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/)。
2. 按一下 hello**計劃**功能表選項。
3. 在 hello 計劃，透過檢視頁面上，按一下 **新增**。
4. 從 hello**訂用帳戶**下拉式清單中，選取 hello 訂用帳戶中的 hello 將位於新的計劃。
5. 從 hello**區域**下拉式清單中，選取 hello 新計劃的區域。 hello 所選區域的 hello 計畫] 選項會顯示在 [hello**計劃選項**hello 頁面區段。
6. 從 hello**資源群組**下拉式清單中，選取資源群組 hello 計劃。 如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。
7. 在**計劃名稱**類型 hello hello 計劃名稱。
8. 在下**計劃選項**，按一下 hello hello 新方案的計費層級。
9. 按一下 [建立] 。

## <a name="deploying-hello-web-service-tooanother-region"></a>部署的 hello web 服務 tooanother 區域
1. 按一下 hello **Web 服務**功能表選項。
2. 選取您要部署 tooa 新區域的 Web 服務的 hello。
3. 按一下 [複製] 。
4. 在**Web 服務名稱**，輸入 hello web 服務的新名稱。
5. 在**Web 服務描述**，輸入 hello web 服務的描述。
6. 從 hello**訂用帳戶**下拉式清單中，選取 hello 訂用帳戶中的 hello 將位於新的 web 服務。
7. 從 hello**資源群組**下拉式清單中，選取資源群組 hello web 服務。 如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。
8. 從 hello**區域**下拉式清單中，選取 hello 哪些 toodeploy hello web 服務中的區域。
9. 從 hello**儲存體帳戶**下拉式清單中，選取儲存體帳戶中哪些 toostore hello web 服務。
10. 從 hello**價格計劃**下拉式清單中，選取您選取在步驟 8 中的 hello 區域中的計劃。
11. 按一下 [複製] 。

