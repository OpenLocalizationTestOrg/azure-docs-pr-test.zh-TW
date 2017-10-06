---
title: "在 Azure 資料目錄中的 aaaManage 資料資產 |Microsoft 文件"
description: "hello 文章重點說明在 Azure 資料目錄中登錄 toocontrol 可見性和資料資產的擁有權的方式。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a>管理 Azure 資料目錄中的資料資產
## <a name="introduction"></a>簡介
Azure 資料目錄是為探索而設計的資料來源，以便您可以輕鬆地找出並了解 hello 資料來源，您需要 tooperform 分析和做出決策。 您與其他使用者可以尋找並了解 hello 大範圍的可用資料來源時，這些探索功能會構成 hello 大影響。 請注意這些項目時，資料目錄 hello 預設行為是針對所有已註冊的資料來源 toobe 可見 tooand 可探索所有目錄使用者。

資料目錄不允許您存取 toohello 資料本身。 Hello hello 資料來源的擁有者所控制的資料存取。 以資料目錄，您可以探索資料來源，並檢視相關的 toohello 來源註冊 hello 目錄中的 hello 中繼資料。

可能的情況下，不過，資料來源只應該儲存可見 toospecific 使用者或特定群組的 toomembers。 在這種情況下，使用者可以取得 hello 目錄中註冊的資料資產的擁有權，然後控制他們所擁有的 hello 資產 hello 可見性。

> [!NOTE]
> 本文中所述的 hello 功能是只在 hello 標準版本的 Azure 資料目錄。 hello 免費版本未提供功能的擁有權，以及限制資料資產可見性。
>
>

## <a name="manage-ownership-of-data-assets"></a>管理資料資產的擁有權
根據預設，資料目錄中註冊的資料資產為無人擁有。 任何具有權限 tooaccess hello 類別目錄的使用者可以探索，並加上註解這些資產。 使用者可以使用未擁有的資料資產的擁有權，並限制他們自己的 hello 資產 hello 可見性。

擁有資料目錄中的資料資產，使用者已獲授權由 hello 擁有者可以找出 hello 資產，並檢視它的中繼資料，並只有 hello 擁有者可以刪除 hello 資產從 hello 類別目錄。

> [!NOTE]
> 在資料目錄中的擁有權會影響儲存在 hello 類別目錄 hello 中繼資料。 擁有權不會授與 hello 基礎資料來源的任何權限。
>
>

### <a name="take-ownership"></a>取得擁有權
使用者可以取得的資料資產的擁有權，藉由選取 hello **Take Ownership** hello 資料目錄入口網站中的選項。 任何特殊權限不是未擁有的資料資產的必要的 tootake 擁有權。 所有使用者都能取得無人擁有之資料資產的擁有權。

### <a name="add-owners-and-co-owners"></a>新增擁有者和共同擁有者
如果資料資產已被人擁有，其他使用者就無法簡單地取得擁有權。 必須由現有擁有者將他們新增為共同擁有者。 任何擁有者都能將其他使用者或安全性群組新增為共同擁有者。

> [!NOTE]
> 它是最佳的作法 toohave 至少兩個人員為擁有者的任何擁有資料資產。
>
>

### <a name="remove-owners"></a>移除擁有者
資產擁有者既然能新增共同擁有者，當然也能移除共同擁有者。

資產擁有者移除本身做為擁有者就無法再管理 hello 資產。 如果 hello 資產擁有者移除本身做為擁有者，而且沒有其他共同擁有者，hello 資產會還原 tooan 未擁有狀態。

## <a name="control-visibility"></a>控制可見性
資料資產擁有者可以控制他們所擁有的 hello 資料資產的 hello 可見性。 hello 預設 toorestrict 可見性，其中所有的資料目錄使用者可以探索和檢視 hello 資料資產 hello 資產擁有者可以切換 hello 可見性設定從**Everyone**太**擁有者與這些使用者** hello hello 資產的內容中。 接著，擁有者便可以新增特定使用者和安全性群組。

> [!NOTE]
> 您應該盡可能 toosecurity 群組和不 tooindividual 使用者應該指派資產的擁有權和可見性的權限。
>
>

## <a name="catalog-administrators"></a>目錄管理員
資料目錄管理員是隱含的 hello 目錄中的所有資產的共同擁有者。 資產擁有者無法移除系統管理員的可見性，而系統管理員可以管理擁有權和 hello 目錄中的所有資料資產的可見度。

## <a name="summary"></a>摘要
hello 資料目錄 crowdsourcing 模型 toometadata 和資料資產探索可讓所有目錄使用者 toocontribute 及探索。 hello 標準版本的資料類別目錄被針對擁有權和管理 toolimit hello 可見性與使用特定的資料資產。
