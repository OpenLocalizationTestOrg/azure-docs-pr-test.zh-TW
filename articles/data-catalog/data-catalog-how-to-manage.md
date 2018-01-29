---
title: "管理 Azure 資料目錄中的資料資產 | Microsoft Docs"
description: "本文專門說明如何控制 Azure 資料目錄中已註冊資料資產的可見性和擁有權。"
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
ms.date: 01/18/2018
ms.author: maroche
ms.openlocfilehash: 5a4b2b5734bf8bfbbc45a65b02362d1fa37b1a87
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="manage-data-assets-in-azure-data-catalog"></a>管理 Azure 資料目錄中的資料資產
## <a name="introduction"></a>簡介
Azure 資料目錄專為資料來源探索功能而設計，讓您能夠輕鬆地探索和了解要執行分析和做出決策所需的資料來源。 當您和其他使用者都能找到並了解最大範圍的可用資料來源時，這些探索功能就能發揮最大效果。 考慮到這些要素，資料目錄的預設行為是要讓所有目錄使用者都能看見並找到所有已註冊的資料來源。

資料目錄並不會讓您存取資料本身。 資料能否存取是由資料來源的擁有者控制。 利用資料目錄，您可以探索資料來源，以及檢視與目錄中註冊的來源相關的中繼資料。

不過，有時候只有特定使用者或特定群組的成員才能看到資料來源。 若是這樣的情況，使用者便可取得目錄中的註冊資料資產的擁有權，然後控制其擁有之資產的可見性。

> [!NOTE]
> 本文所描述的功能只適用於標準版 Azure 資料目錄。 免費版不提供擁有權和限制資料資產可見性的功能。
>
>

## <a name="manage-ownership-of-data-assets"></a>管理資料資產的擁有權
根據預設，資料目錄中註冊的資料資產為無人擁有。 所有具有目錄存取權的使用者都可以探索及標註這些資產。 使用者可以取得無人擁有之資料資產的擁有權，並接著限制其擁有之資產的可見性。

當資料目錄中的資料資產有擁有者時，只有獲得擁有者授權的使用者可以探索資產並檢視其中繼資料，而且只有擁有者可以從目錄中刪除資產。

> [!NOTE]
> 資料目錄中的擁有權只會影響目錄中儲存的中繼資料。 擁有權不會授與任何關於基礎資料來源的權限。
>
>

### <a name="take-ownership"></a>取得擁有權
使用者只要在資料目錄入口網站中選取 [取得擁有權] 選項，就能取得資料資產的擁有權。 取得無人擁有之資料資產的擁有權無需任何特殊權限。 所有使用者都能取得無人擁有之資料資產的擁有權。

### <a name="add-owners-and-co-owners"></a>新增擁有者和共同擁有者
如果資料資產已被人擁有，其他使用者就無法簡單地取得擁有權。 必須由現有擁有者將他們新增為共同擁有者。 任何擁有者都能將其他使用者或安全性群組新增為共同擁有者。

> [!NOTE]
> 已有擁有者的資料資產最好至少有兩個人擔任擁有者。
>
>

### <a name="remove-owners"></a>移除擁有者
資產擁有者既然能新增共同擁有者，當然也能移除共同擁有者。

移除自己之擁有者身分的資產擁有者無法再管理資產。 如果資產擁有者移除自己的擁有者身分，而且已無其他共同擁有者，則資產會回復為無人擁有狀態。

## <a name="control-visibility"></a>控制可見性
資料資產擁有者可以控制其擁有之資料資產的可見性。 若要以預設值限制可見性，讓所有資料目錄使用者都能探索及檢視資料資產，資產擁有者可以將資產屬性中的可見性設定從 [所有人] 切換為 [擁有者與這些使用者]。 接著，擁有者便可以新增特定使用者和安全性群組。

> [!NOTE]
> 請盡可能將資產的擁有權和可見性權限指派給安全性群組而非個別使用者。
>
>

## <a name="catalog-administrators"></a>目錄管理員
資料目錄管理員都是目錄中所有資產的隱含共同擁有者。 資產擁有者無法移除管理員的可見性，而且管理員可以管理目錄中所有資料資產的擁有權和可見性。

## <a name="summary"></a>總結
資料目錄用於中繼資料和資料資產探索的群眾外包模型可讓所有目錄使用者參與和探索。 標準版的資料目錄專為擁有權和管理而設計，可限制特定資料資產的可見性與使用。