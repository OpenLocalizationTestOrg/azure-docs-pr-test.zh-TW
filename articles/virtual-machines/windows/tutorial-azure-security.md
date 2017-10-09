---
title: "在 Azure 中的 aaaAzure 資訊安全中心和 Windows 虛擬機器 |Microsoft 文件"
description: "了解如何使用 Azure 資訊安全中心來確保 Azure Windows 虛擬機器的安全性。"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 238bf4e266a24a536d35dd647db6056ab39a1f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a>使用 Azure 資訊安全中心來監視虛擬機器

Azure 資訊安全中心可協助您了解 Azure 資源的安全性作法。 資訊安全中心提供了整合式的安全性監視功能。 它可以偵測到可能不會被察覺的威脅。 在本教學課程中，您將會了解 Azure 資訊安全中心，以及要如何︰
 
> [!div class="checklist"]
> * 設定資料收集功能
> * 設定安全性原則
> * 檢視及修正組態的健康狀態問題
> * 檢閱所偵測到的威脅  

## <a name="security-center-overview"></a>資訊安全中心概觀

資訊安全中心會找出潛在的虛擬機器 (VM) 組態問題和針對性的安全性威脅。 這些項目可能包括缺少網路安全性群組的 VM、磁碟未加密，以及遠端桌面通訊協定 (RDP) 暴力破解攻擊。 hello 資訊安全中心儀表板中容易閱讀圖表會顯示 hello 資訊。

tooaccess hello 資訊安全中心儀表板，在 Azure 入口網站，在 hello 功能表上，選取 hello**資訊安全中心**。 Hello 儀表板，您可以查看 Azure 環境的 hello 安全性健全狀況、 尋找目前的建議的計數和檢視 hello 的威脅警示的目前狀態。 您可以展開每個高層級圖表 toosee 更多詳細資料。

![資訊安全中心儀表板](./media/tutorial-azure-security/asc-dash.png)

資訊安全中心超出資料探索 tooprovide 建議針對它偵測到的問題。 例如，如果 VM 在部署時未連結網路安全性群組，資訊安全中心便會顯示建議，並指出可供採取的補救步驟。 您不需要離開 hello 內容的資訊安全中心取得自動的補救。  

![建議](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a>設定資料收集功能

您可以查看 VM 安全性組態之前，您會需要 tooset 資訊安全中心資料收集。 這包括開啟資料收集和 Azure 儲存體帳戶 toohold 收集資料。 

1. 在 hello 資訊安全中心儀表板上按一下**安全性原則**，然後選取您的訂用帳戶。 
2. 在 [資料收集] 中選取 [開啟]。
3. toocreate 儲存體帳戶中，選取**選擇儲存體帳戶**。 然後選取 [確定]。
4. 在 hello**安全性原則**刀鋒視窗中，選取**儲存**。 

hello 資訊安全中心資料收集代理程式就會安裝在所有的 Vm，並開始資料收集。 

## <a name="set-up-a-security-policy"></a>設定安全性原則

使用的 toodefine hello 項目為其資訊安全中心會收集資料，並提出建議的安全性原則。 您可以套用不同的安全性原則 toodifferent 組的 Azure 資源。 雖然系統預設會根據所有原則項目來評估 Azure 資源，但您可以針對所有 Azure 資源或某個資源群組來關閉個別的原則項目。 若要深入了解資訊安全中心的安全性原則，請參閱[在 Azure 資訊安全中心設定安全性原則](../../security-center/security-center-policies.md)。 

所有的 Azure 資源的安全性原則 tooset:

1. Hello 資訊安全中心儀表板上選取**安全性原則**，然後選取您的訂用帳戶。
2. 選取 [預防原則]。
3. 開啟或關閉原則項目，您會想 tooapply tooall Azure 資源。
4. 當您選好設定時，請選取 [確定]。
5. 在 hello**安全性原則**刀鋒視窗中，選取**儲存**。 

tooset 特定資源群組的原則：

1. Hello 資訊安全中心儀表板上選取**安全性原則**，然後選取 資源群組。
2. 選取 [預防原則]。
3. 開啟或關閉您要讓 tooapply toohello 資源群組的原則項目。
4. 在 [繼承] 底下選取 [唯一]。
5. 當您選好設定時，請選取 [確定]。
6. 在 hello**安全性原則**刀鋒視窗中，選取**儲存**。  

您也可以在此頁面關閉特定資源群組的資料收集功能。

在下列範例的 hello，唯一的原則已建立名為資源群組的*myResoureGroup*。 此原則會關閉磁碟加密和 Web 應用程式防火牆的建議。

![唯一原則](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a>檢視 VM 組態健康狀態

在您開啟 資料收集，並設定安全性原則之後，資訊安全中心會開始 tooprovide 警示和建議。 部署 Vm，則會安裝 hello 資料收集代理程式。 資訊安全中心接著會填入資料 hello 新 Vm。 若要深入了解 VM 組態的健康狀態，請參閱[在資訊安全中心內保護您的 VM](../../security-center/security-center-virtual-machine-recommendations.md)。 

隨著收集資料，每個 VM 和相關的 Azure 資源的 hello 資源健全狀況彙總。 容易閱讀圖表中會顯示 hello 資訊。 

tooview 資源健全狀況：

1.  Hello 資訊安全中心儀表板上底下**資源安全性健全狀況**，選取**計算**。 
2.  在 hello**計算**刀鋒視窗中，選取**虛擬機器**。 此檢視會為您的 Vm 提供 hello 設定狀態的摘要。

![計算健康狀態](./media/tutorial-azure-security/compute-health.png)

toosee 所有 VM，建議都選取 hello VM。 建議和補救涵蓋 hello 這個教學課程的下一節中詳細說明。

## <a name="remediate-configuration-issues"></a>補救組態問題：

資訊安全中心開始 toopopulate 與設定資料之後，建議都是對根據您設定的 hello 安全性原則。 比方說，如果 VM 設定不含相關聯的網路安全性的群組，提出該項建議的 toocreate 其中一個。 

toosee 所有建議的清單： 

1. Hello 資訊安全中心儀表板上選取**建議**。
2. 選取特定建議。 所有資源的 hello 項建議適用於清單隨即出現。
3. tooapply 建議中，選取特定的資源。 
4. 請依照 hello 補救步驟的指示。 

在許多情況下，資訊安全中心提供可採取動作的步驟可能不需要離開資訊安全中心需要 tooaddress 建議。 在下列範例的 hello，資訊安全中心會偵測具有不受限制的輸入的規則的網路安全性群組。 您可以在 hello 建議頁面上，選取 hello**編輯輸入的規則** 按鈕。 hello 需要的 toomodify hello 規則的 UI 會出現。 

![建議](./media/tutorial-azure-security/remediation.png)

建議在執行補救後會標示為已解決。 

## <a name="view-detected-threats"></a>檢視偵測到的威脅

此外 tooresource 設定建議，資訊安全中心會顯示威脅偵測警示。 hello 安全性警示功能彙總從每個 VM、 Azure 網路的記錄檔和連線的交易夥伴方案 toodetect 對 Azure 資源的安全性威脅所收集的資料。 若要深入了解資訊安全中心的威脅偵測功能，請參閱 [Azure 資訊安全中心的偵測功能](../../security-center/security-center-detection-capabilities.md)。

hello 安全性警示功能需要 hello 資訊安全中心定價層 toobe 從增加*免費*太*標準*。 30 天**免費試用版**時才能使用移動 toothis 較高的定價層。 

toochange hello 定價層：  

1. 在 hello 資訊安全中心儀表板上按一下**安全性原則**，然後選取您的訂用帳戶。
2. 選取 [定價層]。
3. 選取 hello 新的層，然後選取**選取**。
4. 在 hello**安全性原則**刀鋒視窗中，選取**儲存**。 

您已變更定價層的 hello 之後，hello 安全性警示圖形開始 toopopulate 會偵測到安全性威脅。

![安全性警示](./media/tutorial-azure-security/security-alerts.png)

選取警示 tooview 資訊。 例如，您可以看到說明 hello 威脅、 hello 偵測時間、 所有潛在威脅的嘗試，並 hello 建議的補救。 在下列範例的 hello，RDP 暴力攻擊偵測到，與超出 294 嘗試失敗 RDP。 資訊安全中心會提供建議的解決方案。

![RDP 攻擊](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已設定 Azure 資訊安全中心，然後在資訊安全中心檢閱了 VM。 您已了解如何︰

> [!div class="checklist"]
> * 設定資料收集功能
> * 設定安全性原則
> * 檢視及修正組態的健康狀態問題
> * 檢閱所偵測到的威脅

如何使用 Visual Studio Team Services 管線 toocreate CI/CD 以及執行 IIS 的 Windows VM 前進 toohello 下一個教學課程 toolearn。

> [!div class="nextstepaction"]
> [Visual Studio Team Services CI/CD 管線](./tutorial-vsts-iis-cicd.md)
