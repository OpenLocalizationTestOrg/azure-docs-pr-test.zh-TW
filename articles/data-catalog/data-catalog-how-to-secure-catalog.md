---
title: "aaaHow toosecure 存取 tooAzure 資料目錄 |Microsoft 文件"
description: "本文說明如何 toosecure 資料類別目錄和資料資產。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a>Toosecure 存取 toodata 類別目錄和資料資產的方式
> [!IMPORTANT]
> 只在 Azure 資料目錄的 hello standard edition 中使用這項功能。

Azure 資料目錄可讓您 toospecify hello 資料目錄，以及可以存取的人員作業 （註冊、 標註，取得擁有權） 可以在 hello 目錄中的中繼資料上執行。 

## <a name="catalog-users-and-permissions"></a>目錄使用者和權限
toogive 使用者或群組 hello 存取 tooa 資料目錄，並設定權限：

1. 在 [hello[首頁上的資料目錄](http://www.azuredatacatalog.com)，按一下**設定**hello 工具列上。

    ![資料目錄 - 設定](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. 在 [hello] 設定頁面上，展開 [hello**目錄使用者**> 一節。
    ![目錄使用者 - 新增](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)
3. 按一下 [新增] 。
4. 輸入完整的 hello**使用者名**或名稱 hello**安全性群組**hello 與 hello 目錄相關聯的 Azure Active Directory (AAD) 中。 如果您要新增多個使用者或群組，請使用逗號 (`,’) 作為分隔符號。
    ![目錄使用者 - 使用者或群組](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)
5. 按**ENTER**或**] 索引標籤**hello 文字方塊外部。 
6.  確認所有的權限 (**註解**，**註冊**，和**Take Ownership**) 依預設指派 toothese 使用者或群組。 也就是說，hello 使用者或群組可以[註冊資料資產]( data-catalog-how-to-register.md)，[加上註解的資料資產]( data-catalog-how-to-annotate.md)，和[取得擁有權的資料資產]( data-catalog-how-to-manage.md)。 
    ![目錄使用者 - 預設權限](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)
7.  使用者或群組的 toogive hello 讀取存取 toohello 類別目錄中，只清除 hello**加上註解**該使用者或群組的選項。 當您這樣做時，hello 使用者或群組無法標註 hello 目錄中的資料資產，但他們可以檢視它們。 
8.  toodeny 使用者或群組註冊資料資產清除 hello**註冊**該使用者或群組的選項。
9.  使用者從資料資產，清除 hello 的擁有權取得 toodeny**取得擁有權**該使用者或群組的選項。 
10. 按一下 [使用者/群組從目錄使用者 toodelete **x** hello 使用者/群組 hello hello 清單底端。 
    ![目錄使用者 - 刪除使用者](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)

    > [!IMPORTANT]
    > 我們建議您直接加入安全性群組 toocatalog 使用者，而不是新增使用者並指派權限。 然後，加入使用者 toohello 安全性群組符合其角色和其所需的存取 toohello 類別目錄。

## <a name="special-considerations"></a>特殊考量

- hello 權限指派給 toosecurity 群組會加總。 假設使用者位於兩個群組中。 一個群組具有標註權限，而另一個群組沒有標註權限。 那麼，使用者會具有標註權限。 
- 明確指派 tooa 指派的權限 toogroups toowhich hello 使用者所隸屬的使用者覆寫 hello hello 權限。 在 hello 前一個範例中，假設您明確地加入 hello 使用者 toocatalog 使用者和未指派的權限加上註解。 hello 使用者無法標註的資料資產，即使 hello 使用者隸屬的群組，沒有加上註解的權限。

## <a name="next-steps"></a>後續步驟
- [開始使用 Azure 資料目錄](data-catalog-get-started.md)

