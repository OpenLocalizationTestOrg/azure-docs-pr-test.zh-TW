---
title: "命名方針-Linux aaaAzure 基礎結構 |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作命名指導方針 Azure 基礎結構服務中。"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a>適用於 Linux VM 的 Azure 基礎結構命名指導方針 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

本文著重在了解如何針對所有的邏輯和容易識別您各種 Azure 資源 toobuild tooapproach 命名慣例設定的資源整個環境。

## <a name="implementation-guidelines-for-naming-conventions"></a>命名慣例的實作指導方針
决策：

* 哪些是您的 Azure 資源命名慣例？

工作：

* 定義您的資源 toomaintain 一致性 hello affixes toouse。
* 定義指定名稱 hello 需求它們 toobe 全域唯一的儲存體帳戶。
* 文件 hello 命名慣例 toobe 使用，而且將 tooall 合作對象所涉及的 tooensure 一致性分散到部署。

## <a name="naming-conventions"></a>命名慣例
在 Azure 中建立任何項目之前，應先建立良好的命名慣例。 命名慣例可確保所有的 hello 資源都有一個可預測的名稱，可協助降低與管理這些資源相關聯的 hello 系統管理負擔。

您可以選擇 toofollow 一組特定的命名慣例定義整個組織或是特定的 Azure 訂用帳戶或帳戶。 雖然使用 Azure 資源時，它很容易組織 tooestablish 隱含規則內的個人版，您需要 toobe 無法 tooscale 一起工作，在 Azure 中的小組。

預先針對命名慣例組合取得一致的意見。 有些關於命名慣例的考量會牽涉到規則組合。

## <a name="affixes"></a>詞綴
當您檢查 toodefine 命名慣例，一個決策是 hello label 上是否：

* hello 名稱 （前置詞） 的 hello 開頭
* hello hello 名稱 （尾碼） 的結尾

比方說，以下是兩個可能的名稱，資源群組使用 hello`rg`附加：

* Rg-WebApp (前置)
* WebApp-Rg (後置)

Affixes 可以參考描述 hello 特定資源的 toodifferent 層面。 hello 下表顯示一些常用的範例。

| 層面 | 範例 | 注意事項 |
|:--- |:--- |:--- |
| Environment |dev、stg、prod |根據 hello 用途和每個環境的名稱。 |
| 位置 |usw (West US)、use (East US 2) |根據 hello hello 資料中心或 hello hello 組織區域的區域。 |
| Azure 元件、服務或產品 |Rg (適用於資源群組)、VNet (適用於虛擬網路) |根據資源會提供哪些 hello 產品支援。 |
| 角色 |db、app、web |根據 hello hello 虛擬機器角色。 |
| 執行個體 |01、02 和 03 等 |適用於有一個以上執行個體的資源。 例如，雲端服務中負載平衡的 Web 伺服器。 |

在建立您的命名慣例，請確定，它們清楚的 affixes toouse 每種類型的資源，並在哪個位置 （前置詞與尾碼）。

## <a name="dates"></a>日期
它通常是從 hello 名稱建立一個資源重要 toodetermine hello 日期。 我們建議 hello YYYYMMDD 日期格式。 此格式可確保不只是 hello 完整記錄日期，但是該兩個名稱只有在 hello 日期不同的資源也會先依字母順序、 依時間先後順序排序。

## <a name="naming-resources"></a>命名資源
每種類型的資源定義中 hello 命名慣例，其中應該有定義如何 tooassign 名稱 tooeach 資源的規則建立。 這些規則應該套用 tooall 類型的資源，例如：

* 訂用帳戶
* 帳戶
* 儲存體帳戶
* 虛擬網路
* 子網路
* 可用性設定組
* 資源群組
* 虛擬機器
* 端點
* 網路安全性群組
* 角色

hello 名稱的 tooensure 提供它所參考的足夠資訊 toodetermine toowhich 資源，您應該使用描述性的名稱。

## <a name="computer-names"></a>電腦名稱
當您建立虛擬機器 (VM) 時，Azure 需要有 VM 名稱的總 too64 字元用於 hello 資源名稱。 Azure 會使用 hello hello 安裝的作業系統 hello VM 在相同的名稱。 不過，這些名稱可能不一定是 hello 相同。

如果 VM 從已包含作業系統的.vhd 映像檔建立的在 Azure 中的 hello VM 名稱可能不同於 hello VM 的作業系統的電腦名稱。 這種情況下可以加入某種程度的困難 tooVM 管理，因此不建議。 指派 hello Azure VM 資源 hello 相同的名稱，做為您指派該 VM toohello 作業系統 hello 電腦名稱。

我們建議 hello Azure VM 名稱是 hello 與 hello 基礎作業系統的電腦名稱相同。

## <a name="storage-account-names"></a>儲存體帳戶名稱
本節不適太[Azure 受管理磁碟](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，因為您不會建立個別的儲存體帳戶。 對於非受控磁碟，儲存體帳戶具備負責管理其名稱的特殊規則。 您只能使用小寫字母和數字。 如需詳細資訊，請參閱[建立儲存體帳戶](../../storage/storage-create-storage-account.md#create-a-storage-account)。 此外，hello 儲存體帳戶名稱，與 core.windows.net，應該是全域有效且唯一的 DNS 名稱。 比方說，如果 hello 儲存體帳戶呼叫 mystorageaccount，hello 下列產生的 DNS 名稱應該是唯一：

* mystorageaccount.blob.core.windows.net
* mystorageaccount.table.core.windows.net
* mystorageaccount.queue.core.windows.net

## <a name="next-steps"></a>後續步驟
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

