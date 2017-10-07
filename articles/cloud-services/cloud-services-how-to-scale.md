---
title: "aaaAuto hello 傳統入口網站中調整雲端服務 |Microsoft 文件"
description: "（傳統）了解如何 toouse hello 雲端服務 web 角色或背景工作角色在 Azure 傳統入口網站 tooconfigure 自動調整規模規則。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a>如何 tooconfigure 自動調整 hello 傳統入口網站中的雲端服務
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-how-to-scale-portal.md)
> * [Azure 傳統入口網站](cloud-services-how-to-scale.md)

在 hello hello Azure 傳統入口網站的標尺頁面上，您可以設定您的 web 角色或背景工作角色的自動調整規模設定。 或者，您可以設定手動調整，而非規則型自動縮放比例。

> [!NOTE]
> 本文著重於雲端服務 web 和背景工作角色。 當您直接建立虛擬機器 (傳統) 時，它會裝載於雲端服務中。 某些這項資訊適用於 toothese 類型的虛擬機器。 調整虛擬機器的可用性設定組只正在它們開啟和關閉根據您設定的 hello 調整規模規則。 如需有關虛擬機器和可用性設定組的詳細資訊，請參閱[管理 hello 可用性的虛擬機器](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

您應該考慮下列資訊，然後再設定您的應用程式的規模調整 hello:

* 調整受到核心使用量影響。

    較大型的角色執行個體會使用較多核心。 您可以調整應用程式的核心 hello 限制只在您訂用帳戶。 例如，假設您的訂用帳戶有 20 個核心的限制。 如果您使用兩個中型大小的雲端服務 （4 核心總計） 執行應用程式，您可以只向上延展其他雲端服務部署您的訂用帳戶中的 hello 的剩餘 16 個核心。 如需關於大小的詳細資訊，請參閱[雲端服務的大小](cloud-services-sizes-specs.md)。

* 您必須先建立佇列並且將它與角色建立關聯，然後才能根據訊息臨界值調整應用程式。 如需詳細資訊，請參閱[toouse hello 佇列儲存體服務的方式](../storage/queues/storage-dotnet-how-to-use-queues.md)。

* 您可以調整資源的連結的 tooyour 雲端服務。 如需將資源連結的詳細資訊，請參閱[How to： 連結資源 tooa 雲端服務](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service)。

* tooenable 應用程式的高可用性，您應該確定部署與兩個或多個角色執行個體。 如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。

## <a name="schedule-scaling"></a>Schedule scaling
根據預設，所有角色皆未遵循特定的排程。 因此，變更任何設定適用於整個 hello 年的所有日期和 tooall 時間。 如果您想要您可以設定手動或自動縮放比例的 hello 遵循模式的其中一個：

* 工作日
* 週末
* 週間夜
* 週間早上
* 特定日期
* 特定日期範圍

hello 排程會設定在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)上 hello  
[雲端服務] > \[您的雲端服務\] > [調整] > \[生產或預備\] 頁面。

按一下 hello**設定排程時間**按鈕要為每個角色 toochange。

![以排程為基礎的雲端服務自動調整][scale_schedules]

## <a name="manual-scale"></a>手動調整
在 [hello**標尺**] 頁面上，您可以手動增加或減少執行個體的雲端服務中的 hello 數目。 如果您沒有建立排程時，此設定已針對每個已建立的排程或 tooall 時間。

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 **雲端服務**，然後按一下hello hello 雲端服務 tooopen hello 儀表板名稱。
   
   > [!TIP]
   > 如果您沒有看到您的雲端服務，您可能需要從 toochange**生產**太**臨時**，反之亦然。

2. 按一下 [調整] 。
3. 選取您想要擴充選項 toochange hello 排程。 *無法排定的時間*是 hello 預設值，如果您沒有定義的排程。
4. 尋找 hello**依度量調整**區段，然後選取**NONE**。 這項設定是所有角色的 hello 預設值。
5. Hello 雲端服務中的每個角色都有變更的執行個體 toouse hello 號碼的滑桿。
   
    ![手動調整雲端服務角色][manual_scale]
   
    如果您需要更多執行個體，您可能需要 toochange hello[雲端服務的虛擬機器大小](cloud-services-sizes-specs.md)。
6. 按一下 [儲存] 。  
   系統隨即根據您做的選取來新增或移除角色執行個體。

> [!TIP]
> 每當您看到![][tip_icon]移動滑鼠 tooit，您可以取得的特定設定執行作業的相關說明。

## <a name="automatic-scale---cpu"></a>自動調整 - CPU
如果 hello 平均 CPU 使用量百分比高於或低於指定臨界值，可調整此模式。 在這種情況會建立或刪除角色執行個體。

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 **雲端服務**，然後按一下hello hello 雲端服務 tooopen hello 儀表板名稱。
   
   > [!TIP]
   > 如果您沒有看到您的雲端服務，您可能需要從 toochange**生產**太**臨時**，反之亦然。

2. 按一下 [調整] 。
3. 選取您想要擴充選項 toochange hello 排程。 *無法排定的時間*是 hello 預設值，如果您沒有定義的排程。
4. 尋找 hello**依度量調整**區段，然後選取**CPU**。
5. 現在您可以設定最小和最大範圍的角色執行個體、 hello 目標 CPU 使用量 (tootrigger 下向上延展)，以及多少執行個體 tooscale 向上和向下的。

![根據 cpu 負載調整雲端服務角色][cpu_scale]

> [!TIP]
> 每當您看到![][tip_icon]移動滑鼠 tooit，您可以取得的特定設定執行作業的相關說明。

## <a name="automatic-scale---queue"></a>自動調整 - 佇列
如果訊息在佇列中的 hello 數目變成高於或低於指定閾值，自動調整這個模式。 在這種情況會建立或刪除角色執行個體。

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 **雲端服務**，然後按一下hello hello 雲端服務 tooopen hello 儀表板名稱。
   
   > [!TIP]
   > 如果您沒有看到您的雲端服務，您可能需要從 toochange**生產**太**臨時**，反之亦然。

2. 按一下 [調整] 。
3. 尋找 hello**依度量調整**區段，然後選取**佇列**。
4. 現在您可以設定最小和最大範圍的角色執行個體，hello 佇列以及每個執行個體，以及多少執行個體 tooscale 增加和減少的佇列訊息 tooprocess 數目。

![根據訊息佇列調整雲端服務角色][queue_scale]

> [!TIP]
> 每當您看到![][tip_icon]移動滑鼠 tooit，您可以取得的特定設定執行作業的相關說明。

## <a name="scale-linked-resources"></a>調整連結的資源
通常當您調整角色時，它會是有幫助 tooscale hello 資料庫 hello 應用程式也使用。 如果您將連結 hello 資料庫 toohello 雲端服務，您可以存取 hello hello 適當的連結，即可調整該資源的設定。

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 **雲端服務**，然後按一下hello hello 雲端服務 tooopen hello 儀表板名稱。
   
   > [!TIP]
   > 如果您沒有看到您的雲端服務，您可能需要從 toochange**生產**太**臨時**，反之亦然。

2. 按一下 [調整] 。
3. 尋找 hello**已連結的資源**區段，然後按一下**管理此資料庫的調整規模**。
   
   > [!NOTE]
   > 如果您沒有看到 [連結的資源] 區段，您可能沒有任何連結的資源。

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
