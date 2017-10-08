---
title: "Enterprise Integration Pack aaaUsing 憑證 |Microsoft 文件"
description: "了解 toouse 以 hello 企業版整合套件的憑證 |Azure 邏輯應用程式"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a>了解憑證與企業整合套件
## <a name="overview"></a>概觀
企業的整合會使用憑證 toosecure B2B 通訊。 您可以在企業整合應用程式中使用兩種憑證類型：

* 公開憑證，必須先向憑證授權單位 (CA) 購買。
* 私人憑證，您可以自行核發。 這些憑證有時會參照的 tooas 自我簽署的憑證。

## <a name="what-are-certificates"></a>什麼是憑證？
憑證是數位文件，以便驗證 hello 電子通訊中的 hello 參與者的身分識別，也可以保護電子通訊。

## <a name="why-use-certificates"></a>為什麼要使用憑證？
B2B 通訊有時必須確保機密。 企業的整合會使用憑證 toosecure 這些通訊有兩種：

* 藉由加密 hello 訊息的內容
* 以數位方式簽署訊息  

## <a name="upload-a-public-certificate"></a>上傳公開憑證

toouse*公開憑證*B2B 功能與應用程式邏輯，您必須先 tooupload hello 憑證到整合帳戶。  

上傳憑證之後，就可以使用 toohelp hello 中定義其屬性時，安全 B2B 訊息[協議](logic-apps-enterprise-integration-agreements.md)您所建立。  

以下是 hello 您 toohello Azure 入口網站中登入後，將您的公開憑證上傳至整合帳戶的詳細的步驟：

1. 選取**更多服務**輸入**整合**hello 篩選搜尋 方塊中。 選取**整合帳戶**hello 結果清單中     
![選取瀏覽](media/logic-apps-enterprise-integration-certificates/overview-1.png)  
2. 選取您想要 tooadd hello 憑證 hello 整合帳戶 toowhich。  
![選取您想要 tooadd hello 憑證 hello 整合帳戶 toowhich](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. 選取 hello**憑證**磚。  
![選取 hello 憑證磚](media/logic-apps-enterprise-integration-certificates/certificate-1.png)
4. 在 [hello**憑證**刀鋒視窗，開啟時，請選取 hello**新增**] 按鈕。   
![選取 hello [新增] 按鈕](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
5. 輸入**名稱**您的憑證，以及選取 hello 憑證類型為**公用**從 hello 下拉式清單。  
6. 選取 hello 資料夾圖示右邊 hello hello**憑證**文字方塊。 當 hello 檔案選擇器開啟時，尋找並選取您想 tooupload tooyour 整合帳戶 hello 憑證檔案。
7. 選取 hello 憑證，然後選取**確定**hello 檔案選擇器中。 這會驗證，並上傳 hello 憑證 tooyour 整合帳戶。
8. 最後上, 一步 hello**加入憑證**刀鋒視窗中，選取 hello**確定** 按鈕。  
![選取 [確定] 按鈕，hello](media/logic-apps-enterprise-integration-certificates/certificate-3.png)  
9. 選取 hello**憑證**磚。 您應該會看到 hello 新加入的憑證。  
![請參閱 hello 新憑證](media/logic-apps-enterprise-integration-certificates/certificate-4.png)  

## <a name="upload-a-private-certificate"></a>上傳私人憑證

toouse*私用憑證*B2B 功能與應用程式邏輯，您可以上傳的私用憑證 tooyour 整合帳戶採取下列步驟 hello

1. [上傳您私用金鑰 tooKey 保存庫](../key-vault/key-vault-get-started.md "深入了解金鑰保存庫")並提供**機碼名稱** 
   
   > [!TIP]
   > 您必須授權金鑰保存庫的 Logic Apps tooperform 作業。 您可以使用下列 PowerShell 命令的 hello，授與存取 toohello Logic Apps 服務主體：`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`  
   > 
   > 

您已取得 hello 上一個步驟之後，請加入私人憑證 toointegration 帳戶。

下列是 hello 登入 toohello Azure 入口網站之後，將您的私用憑證上傳至整合帳戶的詳細的步驟：  
 
1. 選取您想 tooadd hello 憑證，並選取 hello hello 整合帳戶 toowhich**憑證**磚。  
![選取 hello 憑證磚](media/logic-apps-enterprise-integration-certificates/certificate-1.png)  
2. 在 [hello**憑證**刀鋒視窗，開啟時，請選取 hello**新增**] 按鈕。   
![選取 hello [新增] 按鈕](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
3. 輸入**名稱**您的憑證，以及選取 hello 憑證類型為**私人**從 hello 下拉式清單。   
4. 選取右邊 hello hello hello 資料夾圖示**憑證**文字方塊。 當 hello 檔案選擇器開啟時，找出 hello 對應的公開憑證的 tooupload tooyour 整合帳戶。   
   
   > [!Note]
   > 加入私用憑證時務必 tooadd 對應公用憑證中的 tooshow [AS2 協議](logic-apps-enterprise-integration-as2.md)接收和傳送設定，來簽署與加密 hello 訊息。
   > 
   >   

5. 選取 hello**資源群組**，**金鑰保存庫**，**機碼名稱**和選取 hello**確定** 按鈕。  
![新增憑證](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)  
6. 選取 hello**憑證**磚。 您應該會看到 hello 新加入的憑證。
![請參閱 hello 新憑證](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)  



* [建立 B2B 合約](logic-apps-enterprise-integration-agreements.md)  
* [深入了解金鑰保存庫](../key-vault/key-vault-get-started.md "了解金鑰保存庫")  

