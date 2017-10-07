---
title: "aaaSave 搜尋和 pin 碼在 Azure 資料目錄中的資料資產 |Microsoft 文件"
description: "如何 tooarticle 反白顯示功能，在 Azure 資料目錄中儲存資料來源和資料資產，供日後使用。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a>在 Azure 資料目錄中儲存搜尋和釘選資料資產
## <a name="introduction"></a>簡介
Azure 資料目錄提供用來探索資料來源的功能。 您可以快速搜尋和篩選 hello 目錄 toolocate 資料來源和了解及其預期的用途，讓它更容易 toofind hello 右邊的資料手邊 hello 作業。

但如果您需要 tooregularly 運作以 hello 相同的資料嗎？ 如果您與其他使用者定期未參與知識 toohello hello 目錄中的相同資料來源嗎？ 在這些情況下，有 toorepeatedly 問題 hello 相同搜尋可能會沒有效率。 這是已儲存的搜尋和已釘選的資料資產可發揮作用的地方。

## <a name="saved-searches"></a>已儲存的搜尋
資料目錄中的已儲存搜尋是可重複使用的每個使用者搜尋定義。 您可以定義搜尋，包括搜尋字詞、標籤及其他篩選條件，然後進行儲存。 您可以重新執行 hello 儲存搜尋的定義更新 tooreturn 任何符合其搜尋條件的資料資產。

### <a name="create-a-saved-search"></a>建立已儲存的搜尋
toocreate 儲存的搜尋，請勿 hello 遵循：
1. 在 hello Azure 資料目錄入口網站中 hello**目前搜尋**視窗中，按一下 **儲存**。 

    ![目前搜尋設定的儲存連結](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. 輸入您想 tooreuse，然後再按一下 hello 搜尋準則**儲存**。

    ![目前搜尋設定的已儲存搜尋名稱](./media/data-catalog-how-to-save-pin/02-name.png)

3. 當系統提示您時，輸入 hello 儲存搜尋的名稱。 選取有意義的名稱和描述 hello 將 hello 搜尋所傳回的資料資產。

### <a name="manage-saved-searches"></a>管理已儲存的搜尋
在您儲存一或多個搜尋後**已儲存的搜尋**hello 下方顯示選項**目前搜尋**方塊。 當 hello 清單展開時，會顯示所有已儲存的搜尋。

 ![已儲存的搜尋的清單](./media/data-catalog-how-to-save-pin/03-list.png)

執行 hello 下列任何一項動作：

* tooexecute 搜尋，hello 清單中選取已儲存的搜尋。

* tooview 一份管理選項，將已儲存的搜尋中，按一下向下箭號下一個 toohello 搜尋名稱的 hello。

    ![用於管理已儲存的搜尋的選項](./media/data-catalog-how-to-save-pin/04-managing.png)

* tooenter hello 儲存搜尋的新名稱選取**重新命名**。 hello 搜尋定義不會變更。

* tooremove hello 儲存搜尋清單，請選取**刪除**，然後確認 hello 刪除。

* toomark hello 儲存搜尋，為您的預設搜尋，選取**儲存為預設**。 如果 hello Azure 資料目錄首頁上，您可以執行"empty"的搜尋，則會執行預設的搜尋。 此外，hello 標示為 hello 預設搜尋顯示在 hello hello 最上方的搜尋**已儲存的搜尋**清單。

### <a name="organizational-saved-searches"></a>組織已儲存的搜尋
您組織中的所有使用者都可以儲存搜尋供自己使用。 資料目錄管理員也可以儲存搜尋 hello 組織內的所有使用者。 當系統管理員儲存搜尋時，他們會看到與**hello 公司內共用**選項。 選取此選項共用 hello 儲存 hello 組織中的 搜尋所有使用者。

 ![組織已儲存的搜尋](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a>已釘選的資料資產
利用已儲存的搜尋，您可以儲存並重複使用搜尋定義。 經過一段時間，做為 hello 內容的 hello 目錄變更，可能會變更 hello hello 搜尋所傳回的資料資產。 當您釘選的資料資產時，您可以明確地識別特定的資料資產 toomake 它們更容易 tooaccess 而不需要 toouse 搜尋。

釘選資料資產相當簡單。 tooadd hello 資料資產 tooyour 釘選清單中，您只是按一下 hello **pin**圖示。 hello 資產磚在 hello 並排顯示檢視，和在 hello Azure 資料目錄入口網站中的 hello 清單檢視中的 hello 最左邊資料行中的 hello 角會顯示 hello 圖示。

![hello 資料資產釘選圖示](./media/data-catalog-how-to-save-pin/05-pinning.png)

取消訂選資料資產相當簡單。 只要按一下 hello**取消釘選**hello 選資產的圖示 tootoggle hello 設定。

![hello 資料資產取消釘選圖示](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a>hello 我資產區段
hello 資料目錄入口網站首頁包括**我資產**顯示感興趣 toohello 目前使用者的資產的區段。 此區段同時包含已釘選的資產和已儲存的搜尋。

![hello hello 首頁上的 我的資產區段](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a>摘要
Azure 資料目錄提供功能，可讓您在需要時，更容易的 toodiscover hello 資料來源以便您和其他組織的成員可以花較少尋找資料和使用它的更多時間的時間。 儲存的搜尋 和釘選的資料資產是以這些核心功能為基礎所建立，因此使用者可以輕鬆地識別所要重複使用的資料來源。
