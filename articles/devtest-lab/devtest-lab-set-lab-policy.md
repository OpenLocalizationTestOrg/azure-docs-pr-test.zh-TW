---
title: "在 Azure DevTest Labs aaaManage 實驗室原則 |Microsoft 文件"
description: "深入了解如何 toodefine 實驗室原則，例如 VM 大小，請每位使用者的最大 Vm 和關機自動化。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a>在 Azure DevTest Labs 中管理實驗室的所有原則

Azure DevTest Labs 讓您管理每個實驗室的原則 (設定)，以控制實驗室的成本並儘可能避免浪費。 本文將逐步的詳細說明如何 tooset 每個原則。  

## <a name="set-allowed-virtual-machine-sizes"></a>設定允許的虛擬機器大小
hello 設定 hello 原則允許 VM 大小可協助讓您 toospecify hello 實驗室中允許的 VM 大小會浪費 toominimize 實驗室。 如果啟用這個原則，則只有從此清單中的 VM 大小可以是使用的 toocreate Vm。

1. 在 hello 實驗室**組態和原則**刀鋒視窗中，選取**允許虛擬機器大小**。
   
    ![允許的虛擬機器大小](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. 選取**上**tooenable 此原則，和**關閉**toodisable 它。

1. 如果啟用這個原則，請選取一或多個可在實驗室中建立的 VM 大小。

1. 選取 [ **儲存**]。

## <a name="set-virtual-machines-per-user"></a>設定每位使用者的虛擬機器數目
hello 原則**每位使用者的虛擬機器**可讓您 toospecify hello 的 Vm 數目上限，您可以建立個別的使用者。 如果使用者嘗試 toocreate 或宣告 VM 在達到 hello 使用者限制時，錯誤訊息會指出該 VM 無法建立/宣告的 hello。 

1. 在 hello 實驗室**組態和原則**功能表上，選取**每位使用者的虛擬機器**。
   
    ![每位使用者的虛擬機器數目](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. 選取**是**toolimit hello Vm 數目每位使用者。 如果您不想 toolimit hello Vm 數目每位使用者，選取**否**。 如果您選取**是**，輸入數字值，指出 hello 可建立或由使用者宣告的 Vm 數目上限。 

1. 選取**是**toolimit hello 數目可以使用 SSD （固態磁碟） 的 Vm。 如果您不想 toolimit hello 數目可以使用 SSD 的 Vm，選取**否**。 如果您選取**是**，輸入值，指出 hello 可使用 SSD 來建立的 Vm 數目上限。 

1. 選取 [ **儲存**]。

## <a name="set-virtual-machines-per-lab"></a>設定每個實驗室的虛擬機器數目
hello 原則**每個實驗室的虛擬機器**可讓您 toospecify hello 的 Vm 數目上限可建立 hello 目前實驗室。 如果使用者嘗試 toocreate VM，在達到 hello 實驗室限制時，錯誤訊息指出無法建立 VM 的 hello。 

1. 在 hello 實驗室**組態和原則**功能表上，選取**每個實驗室的虛擬機器**。
   
    ![每個實驗室的虛擬機器數目](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. 選取**是**toolimit hello Vm 數目每個實驗室。 如果您不想 toolimit hello Vm 數目每個實驗室，請選取**否**。 如果您選取**是**，輸入數字值，指出 hello 可建立或由使用者宣告的 Vm 數目上限。 

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

## <a name="set-expiration-date"></a>設定到期日期
您可以設定到期日的日期時您[建立 hello VM](devtest-lab-add-vm.md)。 在**進階設定**，選擇 hello 行事曆圖示 toospecify 日期所在 hello VM 將會自動刪除。  根據預設，永遠不會過期 hello VM。

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>後續步驟
一旦您定義並套用 hello 各種 VM 原則設定您的實驗室，以下是一些事情 tootry 下一步：

* [了解共用的 IP 位址](devtest-lab-shared-ip.md)-說明如何共用的 IP 位址為使用中的公用 IP 位址需要的 tooconnect tooyour 實驗室 Vm 的 DevTest Labs toominimize hello 數目。
* [設定成本管理](devtest-lab-configure-cost-management.md)-說明如何 toouse hello**每月估計成本趨勢**圖表  
  tooview hello 目前月份的估計的成本至今和投射 hello 月底的成本。
* [建立自訂映像](devtest-lab-create-template.md) - 當您建立 VM 時，您要指定一個基本映像，它可以是自訂映像或 Marketplace 映像。 本文說明如何 toocreate 自訂映像從 VHD 檔案。
* [設定 Marketplace 映像](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs 支援根據 Azure Marketplace 映像建立 VM。 本文將說明如何 toospecify 它，如果有的話，可以是 Azure Marketplace 映像在實驗室中建立 Vm 時使用。
* [在實驗室中建立的 VM](devtest-lab-add-vm-with-artifacts.md) -說明如何 toocreate 將 VM 的基本映像從 (可能是自訂或 Marketplace)，以及如何 toowork 連同成品放在 VM 中。

