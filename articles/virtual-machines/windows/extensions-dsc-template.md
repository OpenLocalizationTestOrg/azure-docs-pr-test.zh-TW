---
title: "aaaDesired 狀態設定資源管理員範本 |Microsoft 文件"
description: "Azure 中適用於預期狀態設定的 Resource Manager 範本定義 (包含範例和疑難排解)"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: fc47ac149b1179d9305797eaa8ed8a83c0958c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a>採用 Azure Resource Manager 範本的 Windows VMSS 和預期狀態設定
本文說明 hello 的 hello Resource Manager 範本[Desired State Configuration 延伸模組處理常式](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

## <a name="template-example-for-a-windows-vm"></a>Windows VM 的範本範例
hello 下列程式碼片段會進入 hello hello 範本的資源 > 一節。

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }

```

## <a name="template-example-for-windows-vmss"></a>Windows VMSS 的範本範例
VMSS 節點有一個 「 屬性 」 區段以 hello"VirtualMachineProfile"，"extensionProfile"屬性。 DSC 已加入至 "extensions" 之下。 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
        }
```

## <a name="detailed-settings-information"></a>詳細的設定資訊
hello 下列結構描述是用於 hello 設定部分 hello Azure Resource Manager 範本中的 Azure DSC 延伸模組。

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a>詳細資料
| 屬性名稱 | 類型 | 說明 |
| --- | --- | --- |
| settings.wmfVersion |字串 |指定 hello hello 應該安裝在您的 VM 的 Windows Management Framework 版本。 設定此屬性 too'latest' 安裝 hello 最新版的 WMF。 hello 只有目前可能的值為這個屬性為**'4.0'、 '5.0'，' 5.0PP'，而且 「 最新 」**。 這些可能的值為主體 tooupdates。 hello 預設值為 「 最近的 」。 |
| settings.configuration.url |字串 |指定哪些 toodownload hello URL 位置 DSC 組態 zip 檔案。 如果所提供的 hello URL 需要存取的 SAS 權杖，您需要 tooset hello protectedSettings.configurationUrlSasToken 屬性 toohello 值的 SAS 權杖。 如果已定義 settings.configuration.script 和/或 settings.configuration.function，則需要這個屬性。 |
| settings.configuration.script |字串 |指定 hello hello 指令碼包含 hello 定義 DSC 設定的檔案名稱。 此指令碼必須是 hello hello 從 hello hello configuration.url 屬性所指定之 URL 下載的 zip 檔案的根資料夾中。 如果已定義 settings.configuration.url 和/或 settings.configuration.script，則需要這個屬性。 |
| settings.configuration.function |字串 |指定 hello 的 DSC 設定的名稱。 hello configuration.script 所定義的指令碼中必須包含名為 hello 組態。 如果已定義 settings.configuration.url 和/或 settings.configuration.function，則需要這個屬性。 |
| settings.configurationArguments |集合 |定義您想要 toopass tooyour DSC 設定的所有參數。 這個屬性並未加密。 |
| settings.configurationData.url |字串 |指定從哪個 toodownload 將組態資料 (.psd1) 檔案 toouse 做為輸入 DSC 設定的 hello URL。 如果所提供的 hello URL 需要存取的 SAS 權杖，您需要 tooset hello protectedSettings.configurationDataUrlSasToken 屬性 toohello 值的 SAS 權杖。 |
| settings.privacy.dataEnabled |string |啟用或停用遙測收集。 hello 只可能的值為這個屬性為**'Enable'，'Disable'，'，或 $null**。 將此屬性保持空白或 null 即可啟用遙測。 hello 預設值是 '。 [相關資訊](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| settings.advancedOptions.downloadMappings |集合 |定義從哪些 toodownload hello WMF 的替代位置。 [相關資訊](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| protectedSettings.configurationArguments |集合 |定義您想要 toopass tooyour DSC 設定的所有參數。 這個屬性已加密。 |
| protectedSettings.configurationUrlSasToken |字串 |指定 hello SAS 權杖 tooaccess hello URL configuration.url 所定義。 這個屬性已加密。 |
| protectedSettings.configurationDataUrlSasToken |字串 |指定 hello SAS 權杖 tooaccess hello URL configurationData.url 所定義。 這個屬性已加密。 |

## <a name="settings-vs-protectedsettings"></a>Settings 與ProtectedSettings
所有的設定會儲存在設定文字檔 hello VM 上。
在 [設定] 下的屬性是公用屬性，因為它們不會加密 hello 設定文字檔案中。
'ProtectedSettings' 下的屬性已經使用憑證加密，並不會顯示以 hello VM 上的此檔案中的純文字。

如果 hello 組態需要認證，因此可以包含在 protectedSettings:

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a>範例
hello 以下範例衍生自 hello"Getting Started"區段 hello [DSC 延伸模組處理常式概觀 頁面](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
這個範例會使用資源管理員範本，而不是 cmdlet toodeploy hello 延伸模組。 儲存 hello"IisInstall.ps1 」 設定，請將它放在。ZIP 檔案，以及可存取的 URL 中的上傳 hello 檔案。 這個範例會使用 Azure blob 儲存體，但可能 toodownload。從任意地點使用任意的 ZIP 檔案。

在 hello Azure Resource Manager 範本，hello 下列程式碼會指示 hello VM toodownload hello 正確的檔案並執行 hello 適當的 PowerShell 函式：

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-hello-previous-format"></a>從舊格式 hello 更新
在 hello 舊格式 （包含 hello 公用屬性 ModulesUrl、 ConfigurationFunction、 SasToken 或屬性） 會自動調整 toohello 目前的格式，並如同之前所執行。

下列結構描述的 hello 是何種 hello 先前設定的結構描述看起來像：

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points tooprivate Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
        },
        "ParameterOfTypePSCredential2": {
            "UserName": "UsernameValue2",
            "Password": "PrivateSettingsRef:Key2"
        }
    }
},
"protectedSettings": { 
    "Items": {
        "Key1": "PasswordValue1",
        "Key2": "PasswordValue2"
    },
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

以下是如何 hello 舊格式會調整 toohello 目前的格式：

| 屬性名稱 | 先前結構描述對等項目 |
| --- | --- |
| settings.wmfVersion |settings.wmfVersion |
| settings.configuration.url |settings.ModulesUrl |
| settings.configuration.script |settings.ConfigurationFunction 的第一個部分 ('\\\\' 之前) |
| settings.configuration.function |settings.ConfigurationFunction 的第二個部分 ('\\\\' 之後) |
| settings.configurationArguments |settings.Properties |
| settings.configurationData.url |protectedSettings.DataBlobUri (不含 SAS 權杖) |
| settings.privacy.dataEnabled |settings.privacy.dataEnabled |
| settings.advancedOptions.downloadMappings |settings.advancedOptions.downloadMappings |
| protectedSettings.configurationArguments |protectedSettings.Properties |
| protectedSettings.configurationUrlSasToken |settings.SasToken |
| protectedSettings.configurationDataUrlSasToken |SAS token from protectedSettings.DataBlobUri |

## <a name="troubleshooting---error-code-1100"></a>疑難排解 - 錯誤碼 1100
錯誤代碼 1100 至指出有 hello 使用者輸入 toohello DSC 擴充功能有問題。
這些錯誤的 hello 文字是變數，且可能會變更。
以下是一些您可能會碰到的 hello 錯誤和修正它們。

### <a name="invalid-values"></a>無效的值
「Privacy.dataCollection 為 '{0}'。 hello 只可能的值為 '、 'Enable' 和 'Disable'"「 WmfVersion 為 '{0}'。 可能的值為 … 和 'latest'"

問題︰不允許所提供的值。

解決方案： 變更 hello 有效值 tooa 有效的值。 請參閱 hello 詳細資料 區段中的 hello 資料表。

### <a name="invalid-url"></a>無效的 URL
「ConfigurationData.url 為 '{0}'。 這不是有效的 URL」 「DataBlobUri 為 '{0}'。 這不是有效的 URL」 「Configuration.url 為 '{0}'。 這不是有效的 URL」

問題︰所提供的 URL 無效。

解決方式︰檢查您提供的所有 URL。 請確定所有 Url 都解析 toovalid 位置 hello 延伸模組可以存取 hello 遠端電腦上。

### <a name="invalid-configurationargument-type"></a>無效的 ConfigurationArgument 類型
「無效的 configurationArguments 類型 {0}」

問題： hello ConfigurationArguments 屬性無法解析 tooa Hashtable 物件。 

解決方式︰讓 ConfigurationArguments 屬性變成雜湊表。 請遵循 hello hello 前面範例中所提供的格式。 請留意引號、逗號和括號。

### <a name="duplicate-configurationarguments"></a>重複的 ConfigurationArguments
「在公用和受保護的 configurationArguments 中找到重複的引數 '{0}'」

問題： hello ConfigurationArguments 公用的設定中，而且 hello ConfigurationArguments 受保護的設定中包含以 hello 屬性相同的名稱。

解決方案： 移除其中一個 hello 重複的屬性。

### <a name="missing-properties"></a>遺漏的屬性
「Configuration.function 要求指定 configuration.url 或 configuration.module」

「Configuration.url 要求指定 configuration.script」

「Configuration.script 要求指定 configuration.url」

「Configuration.url 要求指定 configuration.function」

「ConfigurationUrlSasToken 要求指定 configuration.url」

「ConfigurationDataUrlSasToken 要求指定 configurationData.url」

問題︰定義的屬性需要另一個遺漏的屬性。

解決方式︰ 

* 提供 hello 遺漏的屬性。
* 移除 hello 屬性需要 hello 遺漏的屬性。

## <a name="next-steps"></a>後續步驟
深入了解 DSC，以及虛擬機器規模集中[以 hello Azure DSC 延伸模組使用虛擬機器規模集](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)

如需詳細資料，請參閱 [DSC 的安全認證管理](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

如需有關 hello Azure DSC 延伸模組處理常式的詳細資訊，請參閱[簡介 toohello Azure Desired State Configuration 延伸模組處理常式](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

如需有關 PowerShell DSC[造訪 hello PowerShell 文件中心](https://msdn.microsoft.com/powershell/dsc/overview)。 

