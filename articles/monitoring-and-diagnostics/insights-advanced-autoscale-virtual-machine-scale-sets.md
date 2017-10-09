---
title: "使用 Azure 虛擬機器的自動調整規模 aaaAdvanced |Microsoft 文件"
description: "使用 Resource Manager 和 VM 擴展集，搭配多個規則與設定檔，以傳送電子郵件並使用調整動作來呼叫 Webhook URL。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a>針對 VM 擴展集使用 Resource Manager 範本的進階自動調整設定
您可以根據效能標準臨界值、循環排程或特定日期，針對虛擬機器擴展集進行相應縮小和放大。 您也可以針對調整動作設定電子郵件和 webhook 通知。 本逐步解說會示範在 VM 擴展集上使用 Resource Manager 範本設定所有這些物件。

> [!NOTE]
> 雖然這個逐步解說將說明 VM 規模集的 hello 步驟，hello 相同的資訊適用於 tooautoscaling[雲端服務](https://azure.microsoft.com/services/cloud-services/)，和[應用程式服務-Web 應用程式](https://azure.microsoft.com/services/app-service/web/)。
> 簡單標尺 in/out 上虛擬機器擴展集設定為基礎的簡單的效能度量，如 CPU，參閱 toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md)和[Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md)文件
>
>

## <a name="walkthrough"></a>逐步介紹
在此逐步解說中，我們使用[Azure 資源總管](https://resources.azure.com/)擴展集 tooconfigure 和 update hello 自動調整規模設定。 Azure 資源總管是簡單的方式 toomanage 資源管理員範本透過 Azure 資源。 如果您是新 tooAzure 資源總管工具，請參閱[本簡介](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/)。

1. 使用基本自動調整設定部署新的擴展集。 本文使用從 hello Azure 快速入門圖庫具有 Windows hello 其中一個基本的自動調整規模範本與設定小數位數。 Linux 小數位數設定工作 hello 相同的方式。
2. 建立 hello 規模集之後，瀏覽 toohello 小數位數組資源從 Azure 資源總管。 您會看到 hello 下列 Microsoft.Insights 節點下。

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    hello 範本執行已建立預設的自動調整規模設定具有 hello 名稱**'autoscalewad'**。 在 hello 右側，您可以檢視 hello 完整定義，此自動調整規模設定。 在此情況下，CPU %基礎向外延展和向中規則內建 hello 預設自動調整規模設定。  

3. 您現在可以新增多個設定檔和 hello 排程或特定的需求為基礎的規則。 我們會建立具有三個設定檔的自動調整設定。 toounderstand 設定檔及規則中自動調整規模，請先檢閱[自動調整規模的最佳作法](insights-autoscale-best-practices.md)。  

    | 設定檔與規則 | 說明 |
    |--- | --- |
    | **設定檔** |**以效能/計量為基礎** |
    | 規則 |服務匯流排佇列訊息計數 > x |
    | 規則 |服務匯流排佇列訊息計數 < y |
    | 規則 |CPU% > n |
    | 規則 |CPU% < p |
    | **設定檔** |**工作日早上時間 (無規則)** |
    | **設定檔** |**產品發行日 (無規則)** |

4. 以下是我們用於此逐步解說的虛構調整案例。

    * **負載平衡**-我想 tooscale 出或根據應用程式裝載於我的小數位數 set.* hello 負載
    * **訊息佇列大小**-hello 內送訊息 toomy 應用程式使用服務匯流排佇列。 我使用 hello 佇列的訊息計數和 CPU %，而且如果叫用訊息計數或 CPU hello threshold.* 設定預設設定檔 tootrigger 調整規模動作
    * **時間的週次和日子**-我想要每週重複執行 '的時間 hello' 基礎稱為的設定檔 ' 工作日上午 Hours'。 我知道這是較佳 toohave 特定的 VM 執行個體數目 toohandle 我的應用程式負載期間這個 time.* 根據歷程記錄資料，
    * **特殊日期** - 我已新增「產品發行日」設定檔。 我計劃繼續的特定日期因此我的應用程式準備好 toohandle hello 負載行銷公告到期和當我們將新的產品放在 hello application.*
    * *hello 最後兩個設定檔也可以有其他效能度量根據的規則中。在此情況下，我決定不一的 toohave 和 hello 預設效能度量上的 toorely 改為基礎的規則。規則是選擇性的 hello 週期性和日期為基礎的設定檔。*

    自動調整引擎 hello 設定檔和規則的優先順序也會擷取在 hello[自動調整的最佳作法](insights-autoscale-best-practices.md)發行項。
    如需自動調整的常見計量清單，請參閱[自動調整的常用計量](insights-autoscale-common-metrics.md)

5. 請確定您是在 hello**讀/寫**資源總管 中的模式

    ![Autoscalewad, default autoscale setting, 自動調整, 預設自動調整設定](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. 按一下 [編輯]。 **取代**以 hello 下列組態的自動調整規模設定中的 hello '的設定檔 」 項目：

    ![設定檔](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    如需支援的欄位和其值，請參閱[自動調整 REST API 文件](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx)。 現在您的自動調整規模設定包含先前所述的 hello 三個設定檔。

7. 最後，看看 hello 自動調整規模**通知**> 一節。 自動調整規模通知讓您 toodo 三件事，向外延展時，或在動作已成功地在觸發。
   - 通知 hello 系統管理員和共同管理員的訂用帳戶
   - 傳送電子郵件給一組使用者
   - 觸發 webhook 呼叫。 當引發，此 webhook 傳送嗨自動調整條件的相關中繼資料和 hello 規模調整集合資源。 請參閱詳細資料的自動調整規模 webhook hello 裝載 toolearn[設定 Webhook 和自動調整規模的電子郵件通知](insights-autoscale-to-webhook-email.md)。

   新增下列 toohello 自動調整規模設定取代 hello 您**通知**其值為 null 的項目

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]

   ```

   叫用**放**資源總管 tooupdate hello 自動調整規模設定中的按鈕。

您已更新的自動調整規模設定 VM 規模調整集合 tooinclude 上的多個小數位數設定檔，並調整通知。

## <a name="next-steps"></a>後續步驟
使用這些連結 toolearn 深入了解自動調整。

[針對使用虛擬機器擴展集的自動調整進行疑難排解](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[自動調整的常用計量](insights-autoscale-common-metrics.md)

[Azure 自動調整的最佳作法](insights-autoscale-best-practices.md)

[使用 PowerShell 管理自動調整](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[使用 CLI 管理自動調整](insights-cli-samples.md#autoscale)

[針對自動調整設定 Webhook 與電子郵件通知](insights-autoscale-to-webhook-email.md)
