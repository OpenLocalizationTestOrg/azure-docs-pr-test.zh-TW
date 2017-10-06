---
title: "通用 Windows 平台 (UWP) 上行動應用程式使用 aaaCreate |Microsoft 文件"
description: "請遵循此教學課程 tooget 開始使用 Azure 行動應用程式後端在 C#、 Visual Basic 或 JavaScript 開發通用 Windows 平台 (UWP) 應用程式。"
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a>建立 Windows 應用程式
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>概觀
本教學課程會示範如何 tooadd 雲端架構後端服務 tooa 通用 Windows 平台 (UWP) 應用程式。 如需詳細資訊，請參閱 [什麼是 Mobile Apps？](app-service-mobile-value-prop.md)。 hello 下面是從 hello 完成應用程式的螢幕擷取：

![完成的電腦桌面應用程式](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
在電腦桌面上執行。

![完成的手機應用程式](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
在手機上執行

完成本教學課程是 UWP 應用程式的所有其他行動應用程式教學課程的必要條件。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您需要遵循的 hello:

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 Azure 的試用版，並取得向上 too10 可用的行動應用程式，即使您在試用結束後，仍可以繼續使用。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* [Visual Studio Community 2015] 或更新版本。

## <a name="create-a-new-azure-mobile-app-backend"></a>建立新的 Azure 行動應用程式後端
請遵循這些步驟 toocreate 新的行動裝置應用程式後端。

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

您現在已佈建 Azure 行動應用程式後端，可供您的行動用戶端應用程式使用。 接下來，您將會下載 「 todo 清單 」 的簡單的伺服器專案後端，將其發行 tooAzure。

## <a name="configure-hello-server-project"></a>設定 hello 伺服器專案
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a>下載並執行 hello 用戶端專案
一旦您已設定您的行動裝置應用程式後端，您可以建立新的用戶端應用程式，或修改現有的應用程式 tooconnect tooAzure。 本節中，您可以下載為自訂的 tooconnect tooyour 行動裝置應用程式後端的 UWP 應用程式範本專案。

1. 在 hello**快速入門**刀鋒視窗中的行動裝置應用程式後端中，按一下**建立新的應用程式** > **下載**，解壓縮壓縮的 hello 專案檔案tooyour 本機電腦。

    ![下載 Windows 快速入門專案](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. （選擇性）新增 hello UWP 應用程式專案 toohello hello 伺服器專案與相同的方案。 這讓您更輕鬆 toodebug 兩者 hello 應用程式與 hello 後的端中的測試 hello 相同的 Visual Studio 方案中，如果您選擇 toodo 操作。 tooadd UWP 應用程式專案 toohello 方案，您必須使用 Visual Studio 2015 或更新版本。
3. Hello UWP 應用程式為 hello 啟始專案，然後按 hello F5 鍵 toodeploy 和執行的 hello 應用程式。
4. 在 hello 應用程式中，輸入有意義的文字，例如*完成 hello 教學課程*，在 hello**插入 TodoItem**文字方塊，然後再按一下**儲存**。

    ![Windows 快速入門完整桌面](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    這可以傳送 POST 要求 toohello 新行動裝置應用程式的後端裝載在 Azure 中。
5. （選擇性）停止 hello 應用程式，並在不同的裝置或行動模擬器上重新啟動它。

    ![Windows 快速入門完整手機](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    請注意在 hello UWP 應用程式啟動之後，會從 Azure 載入 hello 先前步驟中儲存的資料。

## <a name="next-steps"></a>後續步驟
* [新增驗證 tooyour 應用程式](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  深入了解如何 tooauthenticate 使用者身分識別提供者的應用程式。
* [新增推播通知 tooyour 應用程式](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  了解如何 tooadd 推播通知支援 tooyour 應用程式，並設定行動裝置應用程式後端 toouse Azure 通知中樞 toosend 推播通知。
* [啟用應用程式的離線同步處理](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  了解如何離線 tooadd 支援使用行動裝置應用程式後端應用程式。 離線同步處理可讓使用者使用行動應用程式的 toointeract&mdash;檢視、 加入或修改資料&mdash;即使在沒有網路連線。

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
