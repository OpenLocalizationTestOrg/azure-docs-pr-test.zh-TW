---
title: "aaaUsing Emulator Express toorun 偵錯 Azure 雲端服務在本機電腦上的 |Microsoft 文件"
description: "在 本機電腦上使用 Emulator Express toorun 和偵錯雲端服務"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a>使用 Emulator Express toorun 和偵錯 Azure 雲端服務在本機電腦上
使用 Emulator Express，您可以測試及偵錯雲端服務，而不需以系統管理員身分執行 Visual Studio。 您可以設定您的專案設定 toouse 任一 Emulator Express 或 hello 完整模擬器，視您的雲端服務的 hello 需求而定。 如需 hello 完整模擬器的詳細資訊，請參閱[hello 計算模擬器中執行 Azure 應用程式](storage/common/storage-use-emulator.md)。

## <a name="using-emulator-express-in-visual-studio"></a>在 Visual Studio 中使用 Emulator Express
當您在 Azure SDK 2.3 或更新版本中建立 Azure 專案時，會自動使用 Emulator Express。 使用較早版本的 hello Azure SDK 所建立的現有專案，使用下列步驟 tooselect Emulator Express hello:

1. 在 Visual Studio 中建立或開啟 Azure 雲端服務專案。

1. 在**方案總管 中**、 hello 專案上按一下滑鼠右鍵，然後從 hello 內容功能表中，選取**屬性**。

1. 在 hello 專案屬性頁中，選取 [hello **Web** ] 索引標籤。

    ![Azure 雲端服務專案的屬性](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. 在 [本機程式開發伺服器] 之下，選取 [使用 IIS Express] 選項。

1. 在 [模擬器] 之下，選取 [使用 Emulator Express]。
   
1. toolaunch hello Emulator Express，執行下列命令，在命令提示字元中的 hello: 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Emulator Express 限制
下列問題的 hello 是已知 Emulator Express 的限制： 

- Emulator Express 與「IIS Web 伺服器」不相容。
- 您的雲端服務可包含多個角色，但每個角色都有限的 tooone 執行個體。
- 您無法存取低於 1000 的連接埠號碼。 如果您使用的驗證提供者通常使用低於 1000年的連接埠，您可能需要 toochange 為高於 1000年這個值 tooa 通訊埠編號。
- 套用 toohello Azure 計算模擬器的所有限制也適都用於 tooEmulator Express。 例如，每一個部署不能有 50 個以上的角色執行個體。 如需 hello Azure 計算模擬器的詳細資訊，請參閱[hello 計算模擬器中執行 Azure 應用程式](http://go.microsoft.com/fwlink/p/?LinkId=623050)。

## <a name="next-steps"></a>後續步驟
[進行 Azure 雲端服務偵錯](https://msdn.microsoft.com/library/azure/ee405479.aspx)
