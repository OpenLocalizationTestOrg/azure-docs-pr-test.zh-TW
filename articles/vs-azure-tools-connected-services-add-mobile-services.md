---
title: "使用 Visual Studio 中的 已連接服務 aaaAdding 行動服務 |Microsoft 文件"
description: "將行動服務使用 hello Visual Studio 加入已連接服務對話方塊"
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>使用 Visual Studio 已連接服務加入行動服務
您可以使用 Visual Studio 2015 中，連接 tooAzure 行動服務使用 hello**加入已連接服務**對話方塊。 您可以從任何 C# 用戶端應用程式、任何 JavaScript 應用程式或跨平台 Cordova 應用程式連接。 連接後，您可以建立和存取資料、建立自訂 API 和排程的工作，或加入推播通知的支援。  hello 已連線的服務作業會將加入所有適當的參考和連線程式碼。 您也可以利用包含各種熱門身分識別配置 (例如 Azure AD、Facebook、Twitter 和 Microsoft 帳戶) 的內建驗證支援。

## <a name="supported-project-types"></a>支援的專案類型
> [!NOTE]
> 在 Visual Studio 2015 中，不支援使用 hello 加入已連接服務對話方塊以加入 Azure Mobile Services tooa 通用 Windows (Windows 10) 專案。 您可以藉由安裝 hello 適當封裝使用專案 hello NuGet 封裝管理員新增 Azure 行動服務。
> 
> 

您可以使用 hello 已連接服務對話方塊 tooconnect tooAzure 行動服務中 hello 下列專案類型。

* .NET Windows 8.1 市集、電話和通用應用程式專案
* JavaScript Windows 8.1 市集、電話和通用應用程式專案
* 使用 Visual Studio Tools for Apache Cordova 建立的專案

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a>連接 tooAzure 行動服務使用 hello 加入已連接服務對話方塊
1. 確定您具有 Azure 帳戶。 如果您沒有 Azure 帳戶，您可以註冊 [免費試用](http://go.microsoft.com/fwlink/?LinkId=518146)。
2. 開啟 hello**加入已連接服務** 對話方塊。
   
   * 對於.NET 應用程式中，開啟您的專案在 Visual Studio 中開啟 hello 內容功能表上的 hello**參考**在 方案總管 節點，然後選擇 **加入已連接服務**
     
        ![連接 tooAzure 行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Apache Cordova 應用程式專案中，開啟您的專案在 Visual Studio 中，開啟 hello hello 專案節點，在 方案總管的操作功能表，然後選擇**加入已連接服務**。
3. 在 hello**加入已連接服務**對話方塊方塊中，選擇**Azure Mobile Services**，然後選擇 [hello**設定**] 按鈕。 如果您還沒有，您可能會提示的 toolog 至 Azure。
   
    ![加入 Azure 行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. 在 hello **Azure Mobile Services**對話方塊方塊中，選擇現有行動服務，如果有的話。 如果您需要 toocreate 新的 Azure 行動服務，因此遵循下方 toodo hello 程序。 否則，請略過 toohello 下一個步驟。
   
    toocreate 新的行動服務帳戶：
   
   1. 選擇 hello * * 建立服務 * * 在 hello hello 對話方塊底部的連結。
       ![加入新的已連接行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. 在 hello**建立行動服務**對話方塊中，您可以選擇 JavaScript 後端行動服務或.NET 後端行動服務從 hello**執行階段**下拉式清單。 
      
       ![建立行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       JavaScript 後端服務不但簡單而且功能強大。 如果您建立 JavaScript 後端行動服務，hello 伺服器端 JavaScript 程式碼儲存在 hello 雲端，但您可以使用伺服器總管 中或 hello Azure 管理入口網站編輯伺服器指令碼。 
      
       .NET 後端行動服務可讓您 hello 完整能力及 Web API 和 Entity Framework 的彈性。 如果您建立.NET 後端行動服務時，會為您建立專案，且加入 tooyour 解決方案。 
   3. 選擇 hello**區域**您想 hello 行動服務中，並接著輸入 hello 伺服器使用者名稱和密碼。
   4. 您輸入 hello 所需的所有資訊之後，請選擇 hello**建立**按鈕 toocreate hello 行動服務。
   5. hello 新的行動服務應該會出現在 hello hello 服務清單**Azure Mobile Services**  對話方塊。 在 hello 清單中選擇 hello 新的行動服務，然後選擇 hello**新增**按鈕 tooadd hello 服務 tooyour 專案。
5. 檢閱 hello 快速入門頁面隨即出現，並了解如何修改您的專案。 每當您加入已連接服務時，您的瀏覽器就會出現 [開始使用] 頁面。 您可以檢閱 hello 建議的後續步驟與程式碼範例，或切換 toohello 發生了什麼事頁面 toosee 哪些參考已加入 tooyour 專案，且已修改您的程式碼和組態檔的方式。
6. 使用 hello 程式碼範例做為指南，開始撰寫程式碼 tooaccess 您的行動服務 ！

## <a name="how-your-project-is-modified"></a>您的專案修改方式
Visual Studio 如何修改您的專案相依於 hello 專案類型。 若為 C# 用戶端應用程式，請參閱 [發生什麼情形 – C# 專案](http://go.microsoft.com/fwlink/p/?LinkId=513119)。 若為 JavaScript 用戶端應用程式，請參閱 [發生什麼情形 – JavaScript 專案](http://go.microsoft.com/fwlink/p/?LinkId=513120)。 若為 Cordova 應用程式，請參閱 [發生什麼情形 – Cordova 專案](http://go.microsoft.com/fwlink/p/?LinkId=513116)。

## <a name="next-steps"></a>後續步驟
提出問題並取得協助︰ 

* [MSDN 論壇：Azure 行動服務](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Azure 行動服務在 hello Microsoft Azure 團隊部落格](https://azure.microsoft.com/blog/topics/mobile/)
* [azure.microsoft.com 上的 Azure 行動服務](https://azure.microsoft.com/services/mobile-services/)
* [azure.microsoft.com 上的 Azure 行動服務文件](https://azure.microsoft.com/documentation/services/mobile-services/)

