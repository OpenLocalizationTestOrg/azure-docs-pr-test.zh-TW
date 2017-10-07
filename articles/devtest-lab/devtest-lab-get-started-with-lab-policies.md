---
title: "在 Azure DevTest Labs aaaManage 基本實驗室環境原則 |Microsoft 文件"
description: "深入了解如何 tooset 某些 hello 基本原則 （設定），在 DevTest Labs 實驗室"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a>在 Azure DevTest Labs 中管理實驗室的基本原則

Azure 的 DevTest Labs 可讓您 toocontrol 成本，並減少浪費在實驗室每個實驗室管理原則 （設定）。 本文中，在您開始使用原則學習 tooset 如何當兩個 hello 最關鍵原則-限制 hello 數目的虛擬機器 (VM) 可建立或宣告單一使用者，並設定自動關機。 tooview 如何 tooset 每個實驗室原則，請參閱 hello 文件，[定義中 Azure DevTest Labs 實驗室原則](devtest-lab-set-lab-policy.md)。  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a>在 Azure DevTest Labs 中存取實驗室的原則
hello 下列步驟會引導您設定原則的實驗室中 Azure DevTest Labs:

tooview （與變更） hello 原則的實驗室，請遵循下列步驟：

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。

1. 選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。

1. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。   

1. 選取 [組態和原則]。

    ![[原則設定] 刀鋒視窗](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. hello**組態和原則**刀鋒視窗中包含的設定，您可以指定一個功能表。 本文章涵蓋只 hello 設定**每位使用者的虛擬機器**和**自動關機**。 toolearn 有關 hello 剩餘的設定，請參閱[管理所有原則的實驗室中 Azure DevTest Labs](./devtest-lab-set-lab-policy.md)。 
   
## <a name="set-virtual-machines-per-user"></a>設定每位使用者的虛擬機器數目
hello 原則**每位使用者的虛擬機器**可讓您 toospecify hello 的 Vm 數目上限，您可以建立個別的使用者。 如果使用者嘗試 toocreate 或宣告 VM 在達到 hello 使用者限制時，錯誤訊息會指出該 VM 無法建立/宣告的 hello。 

1. 在 hello 實驗室**組態和原則**功能表上，選取**每位使用者的虛擬機器**。
   
    ![每位使用者的虛擬機器數目](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. 選取**是**toolimit hello Vm 數目每位使用者。 如果您不想 toolimit hello Vm 數目每位使用者，選取**否**。 如果您選取**是**，輸入數字值，指出 hello 可建立或由使用者宣告的 Vm 數目上限。 

1. 選取**是**toolimit hello 數目可以使用 SSD （固態磁碟） 的 Vm。 如果您不想 toolimit hello 數目可以使用 SSD 的 Vm，選取**否**。 如果您選取**是**，輸入值，指出 hello 可使用 SSD 來建立的 Vm 數目上限。 

1. 選取 [ **儲存**]。

## <a name="set-auto-shutdown"></a>設定自動關機
hello 自動關閉原則可幫助 toominimize 實驗室可以讓您在本實驗室 Vm 關機的 toospecify hello 時間會浪費。

1. 在 hello 實驗室**組態和原則**刀鋒視窗中，選取**自動關機**。
   
    ![自動關機](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. 選取**上**tooenable 此原則，和**關閉**toodisable 它。

1. 如果您啟用這個原則，指定下所有 Vm 的 hello 時間 （和時區） tooshut hello 目前實驗室中。

1. 指定**是**或**否**hello 選項 toosend 通知 15 分鐘先前 toohello 指定自動關機時間。 如果您指定**是**，輸入 webhook URL 端點 tooreceive hello 通知。 如需 webhook 的詳細資訊，請參閱[建立 webhook 或 API Azure 函式](../azure-functions/functions-create-a-web-hook-or-api-function.md)。 

1. 選取 [ **儲存**]。

    根據預設，一旦啟用此原則適用於 tooall hello 目前實驗室中的 Vm。 這項設定特定 VM 中，開啟 tooremove hello VM 刀鋒視窗，然後變更其**自動關機**設定 

## <a name="set-auto-start"></a>設定自動啟動
hello 自動啟動原則可讓您 toospecify 時應該啟動 hello 目前實驗室中的 hello Vm。  

1. 在 hello 實驗室**組態和原則**刀鋒視窗中，選取**自動啟動**。
   
    ![自動啟動](./media/devtest-lab-set-lab-policy/auto-start.png)

2. 選取**上**tooenable 此原則，和**關閉**toodisable 它。

3. 如果您啟用這個原則，指定 hello 排定的開始時間、 時區、 和 hello 星期幾 hello 時間適用的 hello。 

4. 選取 [ **儲存**]。

    啟用之後，此原則不會自動套用的 tooany Vm hello 目前實驗室中。 tooapply 這個設定 tooa 特定 VM、 開啟 hello VM 刀鋒視窗，然後變更其**自動啟動**設定 

## <a name="next-steps"></a>後續步驟

- [在 Azure DevTest Labs 中定義實驗室原則](devtest-lab-set-lab-policy.md)-了解如何 toomodify 其他實驗室原則 
