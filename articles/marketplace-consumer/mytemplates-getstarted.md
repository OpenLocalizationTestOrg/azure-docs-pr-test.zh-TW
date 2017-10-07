---
title: "aaaGet 入門私用的範本 |Microsoft 文件"
description: "新增、 管理及共用您的私人範本使用 hello Azure 入口網站、 hello Azure CLI 或 PowerShell。"
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a>開始使用私用 hello Azure 入口網站上的範本
[Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)範本是宣告式的樣板使用 toodefine 您的部署。 您可以定義 hello 資源 toodeploy 解決方案，並指定參數和變數可讓您針對不同的環境 tooinput 值。 hello 範本包含 JSON 和您可以使用運算式 tooconstruct 值為您的部署。

您可以使用 hello 新**範本**功能 hello [Azure 入口網站](https://portal.azure.com)以及 hello **Microsoft.Gallery**資源提供者，來擴充 hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable 使用者 toocreate、 管理及部署個人的程式庫從私用的範本。

本文件將逐步引導您新增、 管理及共用私用**範本**使用 hello Azure 入口網站。

## <a name="guidance"></a>指引
hello 下列建議可協助您充分利用**範本**使用您的方案時：

* **範本** 是一項封裝資源，其中包含 Resource Manager 範本和其他中繼資料。 其行為非常類似 tooan hello Marketplace 中的項目。 hello 主要差異是，它是私用的項目相對於的 toohello 公用 Marketplace 項目。
* hello**範本**適用於使用者需要 toocustomize 其部署的程式庫。
* **範本** 適用於在 Azure 中需要簡單儲存機制的使用者。
* 開始使用現有的 Resource Manager 範本。 在 [github](https://github.com/Azure/azure-quickstart-templates) 中尋找範本，或從現有資源群組[匯出範本](../azure-resource-manager/resource-manager-export-template.md)。
* **範本**是繫結的 toohello 使用者，才能將其發行。 hello 發行者名稱就是擁有讀取權限 tooit 可見 tooeveryone。
* **範本** 是 Resource Manager 資源，一旦發佈便無法重新命名。

## <a name="add-a-template-resource"></a>新增範本資源
有兩種方式 toocreate**範本**hello Azure 入口網站中的資源。

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a>方法 1︰從執行中的資源群組建立新的範本資源
1. 瀏覽 hello Azure 入口網站上的 tooan 現有資源群組。 在 [設定] 中選取 [匯出範本]。
2. 一旦 hello Resource Manager 範本匯出時，使用 hello**儲存範本**按鈕 toosave 它 toohello**範本**儲存機制。 在 [這裡](../azure-resource-manager/resource-manager-export-template.md)尋找匯出範本的完整詳細資料。
   <br /><br />
   ![資源群組匯出](media/rg-export-portal1.PNG)  <br />
3. 選取 hello**儲存 tooTemplate**命令按鈕。
   <br /><br />
4. 輸入下列資訊的 hello:
   
   * 名稱 – hello 範本物件的名稱 (請注意： 這是基礎的 Azure 資源管理員名稱。 適用所有命名限制，一旦建立便無法變更)。
   * 說明-關於 hello 範本的簡短摘要。
     
     ![儲存範本](media/save-template-portal1.PNG)  <br />
5. 按一下 [儲存] 。
   
   > [!NOTE]
   > hello 匯出範本刀鋒視窗中顯示通知時 hello 匯出的資源管理員範本發生錯誤，但是您仍然可以無法 toosave 這個資源管理員範本 toohello 範本。 請確定您檢查並修正任何資源管理員範本問題，才能重新部署的 hello 匯出 Resource Manager 範本。
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a>方法 2 ︰從瀏覽加入新的範本資源
您也可以加入新**範本**使用 hello + 新增] 命令按鈕從頭**瀏覽 > 範本**。 您將需要 tooprovide 描述與 hello Resource Manager 範本 JSON 的名稱。

![新增範本](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> Microsoft.Gallery 是以租用戶為基礎的 Azure 資源提供者。 hello 範本資源是建立它的相等的 toohello 使用者。 不繫結的 tooany 特定訂用帳戶。 訂用帳戶必須 toobe 選擇只有在部署範本。
> 
> 

## <a name="view-template-resources"></a>檢視範本資源
所有**範本**可用 tooyou 可以看到在**瀏覽 > 範本**。 這包括您所建立的**範本**以及利用各種權限層級與您共用的範本。 詳細資料請參閱 hello[存取控制](#access-control-for-a-tenant-resource-provider)下一節。

![檢視範本](media/view-template-portal1.PNG)  <br />

您可以檢視 hello 詳細資料**範本**按 hello 清單中的項目執行。

![檢視範本](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a>編輯範本資源
您可以起始 hello 編輯流程**範本**hello 瀏覽清單上按一下滑鼠右鍵 hello 項目，或是選擇 hello 編輯命令按鈕。

![編輯範本](media/edit-template-portal1a.PNG)  <br />

您可以編輯 hello 描述或資源管理員範本文字。 您無法編輯 hello 名稱，因為它是資源管理員資源的名稱。 當您編輯 hello Resource Manager 範本 JSON 我們將會驗證 tooensure 它是有效的 JSON。 選擇**確定**然後**儲存**toosave 更新的範本。

![編輯範本](media/edit-template-portal2a.PNG)  <br />

一次 hello**範本**會儲存您會看到確認通知。

![編輯範本](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a>部署範本資源
您可以部署任何您有**讀取**權限的**範本**。 hello 部署流程會啟動 hello 標準 Azure 範本部署刀鋒視窗。 填寫 hello 資源管理員範本參數 tooproceed hello 部署的 hello 值。

![部署範本](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a>共用範本資源
可與您的同事共用 **範本** 資源。 共用的行為類似太[Azure 上的任何資源的角色指派](../active-directory/role-based-access-control-configure.md)。 hello**範本**擁有者提供權限可以進行互動的 tooother 使用者範本資源。 hello 個人或群組的人員共用 hello**範本**將能 toosee hello Resource Manager 範本和其組件庫內容。

### <a name="access-control-for-hello-microsoftgallery-resources"></a>Hello Microsoft.Gallery 資源的存取控制
| 角色 | 權限 |
| --- | --- |
| 擁有者 |可讓 hello 樣板資源，包括共用的完整控制 |
| 讀取者 |在 [hello 範本資源上允許的讀取與 Execute(Deploy) |
| 參與者 |Hello 範本資源上允許編輯和刪除權限。 使用者無法與其他人共用 hello 範本 |

選取**共用**hello 瀏覽項目以滑鼠右鍵按一下，或在 hello 特定項目的 [檢視] 刀鋒視窗上。 這會啟動共用經驗。

![共用範本](media/share-template-portal1a.png)  <br />

 您現在可以選擇一種角色和使用者或群組 tooprovide 存取 tooa 特定**範本**。 hello 可用的角色是擁有者、 讀取器和參與者。 詳細資料請參閱 hello[存取控制](#access-control-for-a-tenant-resource-provider)上一節。

![共用範本](media/share-template-portal2b.png)  <br />

![共用範本](media/share-template-portal3b.png)  <br />

按一下 [選取] 和 [確定]。 您現在可以看到 hello 使用者或群組加入 toohello 資源。

![共用範本](media/share-template-portal4b.png)  <br />

> [!NOTE]
> 範本只可共用給使用者和群組 hello 中相同的 Azure Active Directory 租用戶。 如果您不在您的租用戶的電子郵件地址共用範本，將會詢問 hello 做為來賓使用者 toojoin hello 租用傳送邀請。
> 
> 

## <a name="next-steps"></a>後續步驟
* toolearn 有關建立資源管理員範本，請參閱[撰寫範本](../azure-resource-manager/resource-group-authoring-templates.md)
* toounderstand hello 函式，您可以使用資源管理員範本中，請參閱[樣板函式](../azure-resource-manager/resource-group-template-functions.md)
* 如需設計範本的指引，請參閱 [設計 Azure 資源管理員範本的最佳做法](../azure-resource-manager/best-practices-resource-manager-design-templates.md)

