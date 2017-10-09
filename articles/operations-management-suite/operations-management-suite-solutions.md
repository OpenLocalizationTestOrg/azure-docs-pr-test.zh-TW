---
title: "aaaSolutions Operations Management Suite (OMS) |Microsoft 文件"
description: "解決方案會擴充 hello 功能 Operations Management Suite (OMS) 藉由提供封裝的管理案例，客戶可以加入 tootheir OMS 工作區。  本文提供如何自訂客戶和合作夥伴所建立之解決方案的詳細資訊。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5b5a538f1bc4b5577bec94db08bd43668bc6584a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a>在 Operations Management Suite (OMS) 中使用管理解決方案 (預覽)
> [!NOTE]
> 這是 OMS 中管理解決方案 (目前處於預覽狀態) 的預備文件。    
> 
> 

管理解決方案會擴充 hello 功能 Operations Management Suite (OMS) 藉由提供封裝的管理案例，客戶可以加入 tootheir 環境。  此外太[由 Microsoft 提供的解決方案](../log-analytics/log-analytics-add-solutions.md)、 合作夥伴和客戶可以建立自己的環境中使用，或可透過 hello 社群可用 toocustomers 管理解決方案 toobe。

## <a name="finding-and-installing-management-solutions"></a>尋找及安裝管理解決方案
有多個方法來尋找及安裝管理解決方案的更多資訊，hello 下列各節中所述。

### <a name="azure-marketplace"></a>Azure Marketplace
由 Microsoft 提供的管理解決方案，而且受信任的協力廠商可能會安裝從 hello Azure 入口網站中的 hello Azure Marketplace。

1. 登入 toohello Azure 入口網站。
2. Hello 左窗格中，選取**更多服務**。
3. 請向下捲動太**解決方案**或型別*解決方案*到 hello**篩選**對話方塊。
4. 按一下 hello **+ 加** 按鈕。
5. 搜尋您感興趣藉由瀏覽的解決方案按一下 hello**篩選** 按鈕，或輸入 hello**搜尋積木**方塊。
6. 按一下 marketplace 項目 tooview 其詳細的資訊。
7. 按一下**建立**tooopen hello**將方案加入**窗格。
8. 您將會提示的 toorequired 資訊，例如 hello [OMS 工作區以及自動化帳戶](#oms-workspace-and-automation-account)中的任何參數的 toovalues 此外 hello 方案。
9. 按一下**建立**tooinstall hello 方案。

### <a name="oms-portal"></a>OMS 入口網站
由 Microsoft 提供的管理解決方案可能安裝從 hello OMS 入口網站中的 hello 解決方案資源庫。

1. 登入 toohello OMS 入口網站。
2. 按一下 hello**解決方案資源庫**磚。
3. 在 [hello OMS 解決方案資源庫] 頁面上，了解每個可用的解決方案。 按一下您想 tooadd tooOMS hello 方案 hello 名稱。
4. 在您選擇的 hello 解決方案 hello 頁面上，會顯示 hello 方案的詳細的資訊。 按一下 [新增] 。
5. 新建立的磚加入 將顯示在 hello 在 OMS 中的 概觀 頁面上，您便可以開始使用 hello OMS 服務處理資料後的 hello 解決方案。

### <a name="azure-quickstart-templates"></a>Azure 快速入門範本
Hello 社群的成員可以提交管理解決方案 tooAzure 快速入門範本。  您可以下載這些更新版本安裝的範本，或檢查這些 toolearn 如何太[建立您自己的解決方案](#creating-a-solution)。

1. 請依照下列所述的 hello 程序[OMS 工作區以及自動化帳戶](#oms-workspace-and-automation-account)toolink 工作區和帳戶。
2. 跳過[Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。  
3. 搜尋您感興趣的解決方案。
4. 選取 hello 解決方案從 hello 結果 tooview 其詳細資料。
5. 按一下 hello**部署 tooAzure**  按鈕。
6. 系統會提示的 tooprovide 資訊，例如 hello 資源群組和新增 toovalues hello 方案中的任何參數中的位置。
7. 按一下**購買**tooinstall hello 方案。

### <a name="deploy-azure-resource-manager-template"></a>部署 Azure Resource Manager 範本
您收到 hello 社群或您的方案[自行建立](#creating-a-solution)會實作為資源管理員範本，而且您可以使用任何 hello 標準方法[部署範本](../azure-resource-manager/resource-group-template-deploy-portal.md)。  請注意，在安裝之前 hello 方案，您必須建立並連結 hello [OMS 工作區以及自動化帳戶](#oms-workspace-and-automation-account)。

## <a name="oms-workspace-and-automation-account"></a>OMS 工作區和自動化帳戶
大部分的管理解決方案需要[OMS 工作區](../log-analytics/log-analytics-manage-access.md)toocontain 檢視和[自動化帳戶](../automation/automation-security-overview.md#automation-account-overview)toocontain runbook 和相關聯的資源。 hello 工作區中，帳戶必須符合下列需求的 hello。

* 一個解決方案只能使用一個 OMS 工作區和一個自動化帳戶。  
* hello OMS 工作區和自動化解決方案所用的帳戶必須是連結的 tooone 另一個。 OMS 工作區只能連結的 tooone 自動化帳戶，並且自動化帳戶可能只是連結的 tooone OMS 工作區。
* toobe 連結，hello OMS 工作區以及自動化帳戶必須在 hello 相同資源群組和區域。  hello 例外狀況是在美國東部地區的 OMS 工作區，並在美國東部 2 中的自動化帳戶。

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a>建立 OMS 工作區與自動化帳戶之間的連結
如何指定 hello OMS 工作區，並且自動化帳戶取決於您的方案的 hello 安裝方法。

* 當您安裝 Microsoft 解決方案透過 hello OMS 入口網站時，它會安裝在 hello 目前 OMS 工作區，而且沒有任何自動化帳戶需要。
* 當您安裝透過 hello Azure Marketplace 的解決方案時，系統會提示您的 OMS 工作區，以及自動化帳戶和 hello 兩者之間的連結會為您建立。  
* 有外部 hello Azure Marketplace 的解決方案，您必須安裝 hello 解決方案之前連結 hello OMS 工作區以及自動化帳戶。  您可以在 hello Azure Marketplace 中選取任何解決方案，並選取 hello OMS 工作區及自動化帳戶。  您不需要 tooactually 安裝 hello 方案，因為將會建立 hello 連結，為已選取 hello OMS 工作區] 和 [自動化帳戶。  一旦建立 hello 連結，然後您可以使用該 OMS 工作區和自動化帳戶的任何方案。 

### <a name="verifying-hello-link-between-an-oms-workspace-and-automation-account"></a>正在驗證 hello OMS 工作區與自動化帳戶之間的連結
您可以確認 hello OMS 工作區與使用下列程序的 hello 自動化帳戶之間的連結。

1. 選取在 hello Azure 入口網站中的 hello 自動化帳戶。
2. 捲軸 toohello 底部 hello**設定**窗格。
3. 如果沒有呼叫的區段**OMS 資源**在 hello**設定** 窗格中，則此帳戶是附加的 tooan OMS 工作區。
4. 選取**工作區**tooview hello hello OMS 工作區詳細資料連結 toothis 自動化帳戶。

## <a name="listing-management-solutions"></a>列出管理解決方案
使用下列程序 tootooview hello hello 工作區連結 tooyour Azure 訂用帳戶中的管理解決方案的 hello。

1. 登入 toohello Azure 入口網站。
2. Hello 左窗格中，選取**更多服務**。
3. 請向下捲動太**解決方案**或型別*解決方案*到 hello**篩選**對話方塊。
4. 將會列出安裝在您所有工作區中的解決方案。

請注意，您可以檢視 hello 目前工作區中使用 hello OMS 入口網站安裝的唯一 hello Microsoft 解決方案。

## <a name="removing-a-management-solution"></a>移除管理解決方案
移除管理解決方案時，也會移除 hello 方案中的所有資源。  

1. 在 hello Azure 中尋找 hello 方案入口網站的使用中的 hello 程序[列出解決方案](#listing-solutions)。
2. 選取您想要 tooremove hello 解決方案。
3. 按一下 hello**刪除** 按鈕。

## <a name="creating-a-management-solution"></a>建立管理解決方案
[在 Operations Management Suite (OMS) 中建立解決方案](operations-management-suite-solutions-creating.md)提供有關建立管理解決方案的完整指引。 

## <a name="next-steps"></a>後續步驟
* 搜尋 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates)不同 Resource Manager 範本的範例。
* 建立自己的[管理解決方案](operations-management-suite-solutions-creating.md)。

