---
title: "aaaAuto hello 入口網站中調整雲端服務 |Microsoft 文件"
description: "了解如何 toouse hello 雲端服務 web 角色或背景工作角色在 Azure 入口網站 tooconfigure 自動調整規模規則。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a>如何 tooconfigure 自動調整 hello 入口網站中的雲端服務
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-how-to-scale-portal.md)
> * [Azure 傳統入口網站](cloud-services-how-to-scale.md)

針對雲端服務背景工作角色設定條件，以觸發相應縮小或相應放大作業。 hello 角色 hello 條件可以根據 hello CPU、 磁碟或 hello 角色的網路負載。 您也可以設定其他 Azure 資源與您訂用帳戶相關聯的訊息佇列或 hello 標準為基礎的條件。

> [!NOTE]
> 本文著重於雲端服務 web 和背景工作角色。 當您直接建立虛擬機器 (傳統) 時，它會裝載於雲端服務中。 如果要調整標準虛擬機器，您可以將它與[可用性設定組](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)產生關聯，還可以手動開啟或關閉它們。

## <a name="considerations"></a>考量
您應該考慮下列資訊，然後再設定您的應用程式的規模調整 hello:

* 調整受到核心使用量影響。

    較大型的角色執行個體會使用較多核心。 您可以調整應用程式的核心 hello 限制只在您訂用帳戶。 例如，假設您的訂用帳戶有 20 個核心的限制。 如果您使用兩個中型大小的雲端服務 （4 核心總計） 執行應用程式，您可以只向上延展其他雲端服務部署您的訂用帳戶中的 hello 的剩餘 16 個核心。 如需關於大小的詳細資訊，請參閱[雲端服務的大小](cloud-services-sizes-specs.md)。

* 您可以依據佇列訊息臨界值來調整。 如需有關如何 toouse 佇列，請參閱[toouse hello 佇列儲存體服務的方式](../storage/queues/storage-dotnet-how-to-use-queues.md)。

* 您也可以調整與您訂用帳戶相關聯的其他資源。

* tooenable 應用程式的高可用性，您應該確定部署與兩個或多個角色執行個體。 如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。


## <a name="where-scale-is-located"></a>調整所在之處
選取您的雲端服務之後，您應該有 hello 雲端服務刀鋒視窗中顯示。

1. Hello 雲端服務] 刀鋒視窗，在 [hello**角色和執行個體**磚中，選取 hello hello 雲端服務名稱。   
   **重要**： 請確定 tooclick hello 雲端服務角色，不 hello 低於 hello 角色的角色執行個體。

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. 選取 hello**標尺**磚。

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a>自動調整
您可以使用下列任一種模式來設定角色的調整規模設定：**手動**或**自動**。 如您預期為手動時，設定執行個體 hello 絕對計數。 自動但是可讓您 tooset 規則會控制如何及說明更您應該進行調整。

設定 hello**縮放**太選項**排程和效能規則**。

![具有設定檔與規則的雲端服務調整規模設定](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. 現有的設定檔。
2. 加入 hello 父系設定檔的規則。
3. 新增另一個設定檔。

選取 [新增設定檔]。 hello 設定檔會決定哪一種模式要 hello 標尺的 toouse:**一律**，**循環**，**固定日期**。

您已設定 hello 設定檔和規則之後，請選取 hello**儲存**hello 上方的圖示。

#### <a name="profile"></a>設定檔
hello 設定檔設定最小和最大執行個體的 hello 調整，而且也時這個標尺範圍作用中。

* **一律**

    一律讓此範圍的執行個體個數保持可用狀態。  

    ![一律調整的雲端服務](./media/cloud-services-how-to-scale-portal/select-always.png)
* **週期性**

    選擇一組天數的 hello 週 tooscale。

    ![具有週期性排程的雲端服務調整規模](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* **固定日期**

    固定的日期範圍 tooscale hello 角色。

    ![具有固定日期的雲端服務調整規模](./media/cloud-services-how-to-scale-portal/select-fixed.png)

您已設定 hello 設定檔之後，請選取 hello**確定**在 hello hello 設定檔 刀鋒視窗底部的按鈕。

#### <a name="rule"></a>規則
規則會加入 tooa 設定檔，並代表觸發程序 hello 小數位數的條件。

hello 規則觸發程序為基礎的 hello 雲端服務 （CPU 使用量、 磁碟活動或網路活動） 的度量 toowhich 您可以加入條件式值。 此外，您可以根據其他 Azure 資源與您訂用帳戶相關聯的訊息佇列或 hello 度量 hello 觸發程序。

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

您已設定 hello 規則之後，請選取 hello**確定**在 hello hello 規則刀鋒視窗底部的按鈕。

## <a name="back-toomanual-scale"></a>備份 toomanual 小數位數
瀏覽 toohello[縮放設定](#where-scale-is-located)組 hello 和**縮放**太選項**手動輸入執行個體計數**。

![具有設定檔與規則的雲端服務調整規模設定](./media/cloud-services-how-to-scale-portal/manual-basics.png)

這個設定會移除從 hello 角色自動縮放比例，然後直接設定 hello 執行個體計數。

1. hello 小數位數 （手動或自動） 選項。
2. 角色執行個體滑桿 tooset hello 執行個體至 tooscale。
3. Hello 角色 tooscale 到的執行個體。

您已設定 hello 調整規模設定之後，請選取 hello**儲存**hello 上方的圖示。
