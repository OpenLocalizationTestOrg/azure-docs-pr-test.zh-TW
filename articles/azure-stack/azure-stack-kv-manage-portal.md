---
title: "使用 PowerShell 的 Azure 堆疊中的金鑰保存庫 aaaManage |Microsoft 文件"
description: "深入了解如何使用 PowerShell 的 Azure 堆疊中的金鑰保存庫 toomanage。"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 0a3aa6eb0b2c2976935d995a0bf6f226dc4eac84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-hello-portal"></a>管理 Azure 堆疊使用 hello 入口網站中的金鑰保存庫

您可以使用 hello Azure 堆疊入口網站來管理 Azure 堆疊中的金鑰保存庫。 這篇文章可協助您取得啟動的 toocreate 並管理 Azure 堆疊中的金鑰保存庫。 

## <a name="prerequisites"></a>必要條件  

* Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含 hello 金鑰保存庫服務。  
* 使用者必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)包含 hello 金鑰保存庫服務。  
 
## <a name="create-a-key-vault"></a>建立金鑰保存庫 

1. 登入 toohello 使用者入口網站 (https://portal.local.azurestack.external)。  

2. 從 hello 儀表板中，按一下 **新增 > 安全性 + 身分識別 > 金鑰保存庫**。  

    ![KV 畫面](media/azure-stack-kv-manage-portal/image1.png)  

3. 在 hello**建立金鑰保存庫**刀鋒視窗中，指派**名稱**您保存庫。 保存庫名稱只能包含英數字元、 hello 特殊字元連字號 （-），而且不應該以開頭數字。  

4. 選擇**訂用帳戶**從 hello 可用訂閱清單。 提供 hello 金鑰保存庫服務的所有訂用帳戶會顯示在 [hello] 下拉式清單中。  

5. 選取現有的 [資源群組] 或建立新群組。  

6. 選取 hello**定價層**。  
    >[!NOTE]
    > Azure Stack 開發套件中的金鑰保存庫僅支援**標準**SKU。

7. 選取現有的 [存取原則] 或建立新原則。 存取原則可讓您 toogrant 使用者、 應用程式或安全性權限群組 tooperform 作業與此保存庫。  

8. （選擇性） 選擇**進階存取權原則**tooenable hello 功能，例如存取 tooVirtual 機器進行部署，存取 tooResource 管理員針對範本部署，以及存取 tooAzure 磁碟加密磁碟區加密。 
  
9.  設定 hello，完成後，按一下 **確定**然後**建立**。 這樣會啟動 hello 金鑰保存庫部署。 

## <a name="manage-keys-and-secrets"></a>管理金鑰和祕密

建立保存庫之後，請使用下列步驟 toocreate hello，以及管理金鑰和秘密 hello 保存庫中。

## <a name="create-a-key"></a>建立金鑰

1. 登入 toohello 使用者入口網站 (https://portal.local.azurestack.external)。  

2. 從 hello 儀表板中，按一下 **所有資源**> 您先前建立的選取 hello 金鑰保存庫 > 按一下 hello**金鑰**磚。  

3. 從 hello**金鑰**刀鋒視窗中，按一下 **新增**。 

4. 在 hello**建立金鑰**刀鋒視窗中，表單 hello 清單**選項**，選擇 hello 方法您想 toouse toocreate 索引鍵。 您可以 [產生] 新的金鑰、[上傳] 現有金鑰，或是 [還原備份] 金鑰。  

5. 在 [名稱] 中輸入金鑰的名稱。 hello 索引鍵名稱只能包含英數字元和 hello 特殊字元連字號 （-）。  

6. (選用) 為金鑰設定 [設定啟用日期] 和 [設定到期日期]。  

7. 按一下**建立**toostart hello 部署。  

已成功建立 hello 金鑰之後，可以選取從 hello**金鑰**刀鋒視窗和檢視或修改其屬性。 hello properties 區段包含 hello**金鑰識別碼**，外部應用程式可以存取此機碼的 URI。 此機碼 toolimit 作業下設定設定**允許的作業**。

![URI 金鑰](media/azure-stack-kv-manage-portal/image4.png)  

## <a name="create-a-secret"></a>建立祕密 

1. 登入 toohello 使用者入口網站 (https://portal.local.azurestack.external)。  
2. 從 hello 儀表板中，按一下 **所有資源**> 您先前建立的選取 hello 金鑰保存庫 > 按一下 hello**密碼**磚。  

3. 從 hello**密碼**刀鋒視窗中，按一下 **新增**。  

4. 在 hello**建立密碼**刀鋒視窗中的，從 hello 清單**上傳選項**，選擇要依據的 toocreate 選項的密碼。 您可以建立密碼**手動**hello 密碼的輸入值，或上傳**憑證**從本機電腦。  

5. 輸入**名稱**的 hello 密碼。 hello 秘密名稱只能包含英數字元和 hello 特殊字元連字號 （-）。  

6. （選擇性） 指定 hello**內容類型**，以及設定值**設定啟用日期**和**設定到期日**hello 密碼的值。  

7. 按一下 建立 toostart hello 部署。  

已成功建立 hello 密碼之後，可以選取從 hello**密碼**刀鋒視窗和檢視或修改其屬性。 hello properties 區段包含**密碼識別碼**，外部應用程式可以存取此密碼的 URI。 

![URI 祕密](media/azure-stack-kv-manage-portal/image5.png) 


## <a name="next-steps"></a>後續步驟
* [擷取儲存在金鑰保存庫中的 hello 密碼來部署 VM](azure-stack-kv-deploy-vm-with-secret.md)  
* [使用存放在金鑰保存庫中的憑證來部署虛擬機器](azure-stack-kv-push-secret-into-vm.md)     


