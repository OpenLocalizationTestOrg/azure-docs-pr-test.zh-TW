---
title: "設定具名驗證認證 aaaSetting |Microsoft 文件"
description: "了解 Visual Studio 可以使用 tooauthenticate 要求 tooAzure toopublish 從 Visual Studio 或 toomonitor 的現有應用程式 tooAzure tootooprovide 認證如何雲端服務... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a>設定具名的驗證認證
從 Visual Studio 或 toomonitor 現有的雲端服務應用程式 tooAzure toopublish 中，您必須提供認證，Visual Studio 可以使用 tooauthenticate 要求 tooAzure。 有幾個位置，在 Visual Studio 中，您可以登入 tooprovide 中這些認證。 例如，hello 伺服器總管] 中，您可以從開啟 hello 的 hello 快顯功能表**Azure**節點，然後選擇 [**連接 tooMicrosoft Azure 訂用帳戶...**.當您登入時，hello 與您的 Azure 帳戶相關聯的訂用帳戶資訊使用在 Visual Studio 中，沒有任何多個具有 toodo。

Azure Tools 還支援提供的認證，較舊的方式使用 hello 訂用帳戶檔案 （.publishsettings 檔案）。 本主題將說明此方法，Azure SDK 2.2 中仍支援此方法。

hello 下列項目所需的驗證 tooAzure:

* 訂用帳戶識別碼
* 有效的 X.509 v3 憑證

> [!NOTE]
> hello hello X.509 v3 憑證的金鑰長度必須至少為 2048 個位元。 Azure 將會拒絕任何不符合此需求或無效的憑證。
>
>

Visual Studio 會使用您的訂用帳戶 ID 與 hello 憑證資料一起做為認證。 hello 適當的認證會在 hello 訂用帳戶檔案 （.publishsettings 檔案），其中包含公開金鑰 hello 憑證參考。 hello 訂閱檔案可以包含多個訂用帳戶的認證。

您可以編輯 hello 訂用帳戶資訊從 hello**新增/編輯訂用帳戶**對話方塊中，在本主題稍後所述。

如果您想 toocreate 憑證自己，您可以參考中的 toohello 指示[建立及上傳 Azure 的管理憑證](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx)然後再手動上傳 hello 憑證 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!NOTE]
> Visual Studio 需要您的雲端服務不是的 toomanage 這些認證 hello 必要的 tooauthenticate 的相同認證對 hello Azure 儲存體服務提出的要求。
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a>在 Visual Studio 中設匯入、設定或編輯驗證認證
您可以匯入、 設定，或修改您的驗證認證，在 hello**新訂用帳戶**對話方塊中，會顯示您執行下列動作的 hello:

* 在**伺服器總管**，開啟 hello 的 hello 快顯功能表**Azure**  節點，選擇**管理和篩選訂閱...**，選擇 hello**憑證**索引標籤，然後執行 hello 下列其中一種：

    * 選擇**匯入**tooopen hello 匯入的 Microsoft Azure 訂用帳戶 對話方塊，您可以下載 hello 的 hello 訂用帳戶檔案目前載入的訂用帳戶中，瀏覽 tooits 下載位置，並將它匯入，以用於驗證。
    * 選擇**新增**tooopen hello 新訂用帳戶 對話方塊，您可以設定用於驗證的新訂閱。
    * 選擇**編輯**（之後，選擇您的作用中訂用帳戶） tooopen hello 編輯訂用帳戶 對話方塊，您可以編輯用於驗證現有的訂閱。 

hello 下列程序會假設該 hello**新訂用帳戶**對話方塊為開啟。

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a>在 Visual Studio 中的驗證認證 tooset
1. 在 [hello**選取現有憑證**驗證] 清單中，選擇憑證。
2. 選擇 hello**複製 hello 完整路徑**連結。 hello 憑證 （.cer 檔案） 的 hello 路徑是複製的 toohello 剪貼簿。

   > [!IMPORTANT]
   > toopublish Azure 應用程式從 Visual Studio 中，您必須上傳此憑證 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
   >
   >
3. tooupload hello 憑證 toohello Azure 入口網站：

   1. 開啟 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
   2. 如果出現提示，請登入 toohello 入口網站，然後瀏覽過**設定**，**管理憑證**。
   3. 在 hello 管理憑證 窗格中，選擇 **上傳**。
   4. 選取您的 Azure 訂閱，貼上 hello 剛 hello.cer 檔案的完整路徑建立，並選擇**上傳**。
