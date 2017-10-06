---
title: "aaaAccessing 私人 Azure 的雲端與 Visual Studio |Microsoft 文件"
description: "了解如何 tooaccess 私人雲端使用 Visual Studio 的資源。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>使用 Visual Studio 存取 Azure 私人雲端
根據預設，Visual Studio 支援 Azure 公用雲端 REST 端點。 在本主題中，您學會如何 toouse 您的私人雲端的憑證 tooaccess-和互動-hello 從 Visual Studio 的私人雲端。

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a>在 Visual Studio 中的 tooaccess 私人 Azure 雲端
1. 在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)hello 私人雲端，下載您的發行設定檔，或連絡您的系統管理員發行設定檔。 在 Azure 的 hello 公用版本，hello 這是連結 toodownload [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/)。 (hello 下載的檔案應該有的擴充功能`.publishsettings`)

1. 開啟 Visual Studio

1. 在**伺服器總管**，以滑鼠右鍵按一下 hello **Azure**節點，然後從 hello 內容功能表中，選取**管理和篩選訂閱**。
   
    ![管理訂用帳戶命令](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. 在 hello**管理 Microsoft Azure 訂用帳戶**對話方塊中，選取 hello**憑證**索引標籤，然後選取**匯入**。
   
    ![正在匯入 Azure 憑證](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. 在 hello**匯入 Microsoft Azure 訂用帳戶**對話方塊中，選取**瀏覽**。

    ![瀏覽在 hello 匯入 Microsoft Azure 訂用帳戶 對話方塊上的按鈕](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. 在 [hello**開啟**] 對話方塊中，您已儲存的 hello 發行設定檔，請選取 hello 檔案，其中的目錄，然後選取瀏覽 toohello**開啟**。

    ![選取 hello 發佈設定檔](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. 當傳回 toohello**匯入 Microsoft Azure 訂用帳戶**對話方塊中，選取**匯入**。

    ![匯入 hello 發佈設定檔](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    hello 憑證從 hello 發佈設定檔匯入 Visual Studio 中，您現在可以與私人雲端資源互動。
   
## <a name="next-steps"></a>後續步驟
- [發行 tooan Azure 雲端服務，從 Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- [如何：下載和匯入發佈設定和訂用帳戶資訊](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)
