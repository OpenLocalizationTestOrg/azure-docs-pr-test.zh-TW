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
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="c6700-103">採用 Azure Resource Manager 範本的 Windows VMSS 和預期狀態設定</span><span class="sxs-lookup"><span data-stu-id="c6700-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="c6700-104">本文說明 hello 的 hello Resource Manager 範本[Desired State Configuration 延伸模組處理常式](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c6700-104">This article describes hello Resource Manager template for hello [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="c6700-105">Windows VM 的範本範例</span><span class="sxs-lookup"><span data-stu-id="c6700-105">Template example for a Windows VM</span></span>
<span data-ttu-id="c6700-106">hello 下列程式碼片段會進入 hello hello 範本的資源 > 一節。</span><span class="sxs-lookup"><span data-stu-id="c6700-106">hello following snippet goes into hello Resource section of hello template.</span></span>

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

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="c6700-107">Windows VMSS 的範本範例</span><span class="sxs-lookup"><span data-stu-id="c6700-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="c6700-108">VMSS 節點有一個 「 屬性 」 區段以 hello"VirtualMachineProfile"，"extensionProfile"屬性。</span><span class="sxs-lookup"><span data-stu-id="c6700-108">A VMSS node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="c6700-109">DSC 已加入至 "extensions" 之下。</span><span class="sxs-lookup"><span data-stu-id="c6700-109">DSC is added under "extensions".</span></span> 

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

## <a name="detailed-settings-information"></a><span data-ttu-id="c6700-110">詳細的設定資訊</span><span class="sxs-lookup"><span data-stu-id="c6700-110">Detailed Settings Information</span></span>
<span data-ttu-id="c6700-111">hello 下列結構描述是用於 hello 設定部分 hello Azure Resource Manager 範本中的 Azure DSC 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="c6700-111">hello following schema is for hello settings portion of hello Azure DSC extension in an Azure Resource Manager template.</span></span>

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

## <a name="details"></a><span data-ttu-id="c6700-112">詳細資料</span><span class="sxs-lookup"><span data-stu-id="c6700-112">Details</span></span>
| <span data-ttu-id="c6700-113">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c6700-113">Property Name</span></span> | <span data-ttu-id="c6700-114">類型</span><span class="sxs-lookup"><span data-stu-id="c6700-114">Type</span></span> | <span data-ttu-id="c6700-115">說明</span><span class="sxs-lookup"><span data-stu-id="c6700-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6700-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="c6700-116">settings.wmfVersion</span></span> |<span data-ttu-id="c6700-117">字串</span><span class="sxs-lookup"><span data-stu-id="c6700-117">string</span></span> |<span data-ttu-id="c6700-118">指定 hello hello 應該安裝在您的 VM 的 Windows Management Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="c6700-118">Specifies hello version of hello Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="c6700-119">設定此屬性 too'latest' 安裝 hello 最新版的 WMF。</span><span class="sxs-lookup"><span data-stu-id="c6700-119">Setting this property too'latest' installs hello most updated version of WMF.</span></span> <span data-ttu-id="c6700-120">hello 只有目前可能的值為這個屬性為**'4.0'、 '5.0'，' 5.0PP'，而且 「 最新 」**。</span><span class="sxs-lookup"><span data-stu-id="c6700-120">hello only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="c6700-121">這些可能的值為主體 tooupdates。</span><span class="sxs-lookup"><span data-stu-id="c6700-121">These possible values are subject tooupdates.</span></span> <span data-ttu-id="c6700-122">hello 預設值為 「 最近的 」。</span><span class="sxs-lookup"><span data-stu-id="c6700-122">hello default value is 'latest'.</span></span> |
| <span data-ttu-id="c6700-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="c6700-123">settings.configuration.url</span></span> |<span data-ttu-id="c6700-124">字串</span><span class="sxs-lookup"><span data-stu-id="c6700-124">string</span></span> |<span data-ttu-id="c6700-125">指定哪些 toodownload hello URL 位置 DSC 組態 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6700-125">Specifies hello URL location from which toodownload your DSC configuration zip file.</span></span> <span data-ttu-id="c6700-126">如果所提供的 hello URL 需要存取的 SAS 權杖，您需要 tooset hello protectedSettings.configurationUrlSasToken 屬性 toohello 值的 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="c6700-126">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationUrlSasToken property toohello value of your SAS token.</span></span> <span data-ttu-id="c6700-127">如果已定義 settings.configuration.script 和/或 settings.configuration.function，則需要這個屬性。</span><span class="sxs-lookup"><span data-stu-id="c6700-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="c6700-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="c6700-128">settings.configuration.script</span></span> |<span data-ttu-id="c6700-129">字串</span><span class="sxs-lookup"><span data-stu-id="c6700-129">string</span></span> |<span data-ttu-id="c6700-130">指定 hello hello 指令碼包含 hello 定義 DSC 設定的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="c6700-130">Specifies hello file name of hello script that contains hello definition of your DSC configuration.</span></span> <span data-ttu-id="c6700-131">此指令碼必須是 hello hello 從 hello hello configuration.url 屬性所指定之 URL 下載的 zip 檔案的根資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c6700-131">This script must be in hello root folder of hello zip file downloaded from hello URL specified by hello configuration.url property.</span></span> <span data-ttu-id="c6700-132">如果已定義 settings.configuration.url 和/或 settings.configuration.script，則需要這個屬性。</span><span class="sxs-lookup"><span data-stu-id="c6700-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="c6700-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="c6700-133">settings.configuration.function</span></span> |<span data-ttu-id="c6700-134">字串</span><span class="sxs-lookup"><span data-stu-id="c6700-134">string</span></span> |<span data-ttu-id="c6700-135">指定 hello 的 DSC 設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="c6700-135">Specifies hello name of your DSC configuration.</span></span> <span data-ttu-id="c6700-136">hello configuration.script 所定義的指令碼中必須包含名為 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="c6700-136">hello configuration named must be contained in hello script defined by configuration.script.</span></span> <span data-ttu-id="c6700-137">如果已定義 settings.configuration.url 和/或 settings.configuration.function，則需要這個屬性。</span><span class="sxs-lookup"><span data-stu-id="c6700-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="c6700-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c6700-138">settings.configurationArguments</span></span> |<span data-ttu-id="c6700-139">集合</span><span class="sxs-lookup"><span data-stu-id="c6700-139">Collection</span></span> |<span data-ttu-id="c6700-140">定義您想要 toopass tooyour DSC 設定的所有參數。</span><span class="sxs-lookup"><span data-stu-id="c6700-140">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="c6700-141">這個屬性並未加密。</span><span class="sxs-lookup"><span data-stu-id="c6700-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="c6700-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="c6700-142">settings.configurationData.url</span></span> |<span data-ttu-id="c6700-143">字串</span><span class="sxs-lookup"><span data-stu-id="c6700-143">string</span></span> |<span data-ttu-id="c6700-144">指定從哪個 toodownload 將組態資料 (.psd1) 檔案 toouse 做為輸入 DSC 設定的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="c6700-144">Specifies hello URL from which toodownload your configuration data (.psd1) file toouse as input for your DSC configuration.</span></span> <span data-ttu-id="c6700-145">如果所提供的 hello URL 需要存取的 SAS 權杖，您需要 tooset hello protectedSettings.configurationDataUrlSasToken 屬性 toohello 值的 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="c6700-145">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationDataUrlSasToken property toohello value of your SAS token.</span></span> |
| <span data-ttu-id="c6700-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="c6700-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="c6700-147">string</span><span class="sxs-lookup"><span data-stu-id="c6700-147">string</span></span> |<span data-ttu-id="c6700-148">啟用或停用遙測收集。</span><span class="sxs-lookup"><span data-stu-id="c6700-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="c6700-149">hello 只可能的值為這個屬性為**'Enable'，'Disable'，'，或 $null**。</span><span class="sxs-lookup"><span data-stu-id="c6700-149">hello only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="c6700-150">將此屬性保持空白或 null 即可啟用遙測。</span><span class="sxs-lookup"><span data-stu-id="c6700-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="c6700-151">hello 預設值是 '。</span><span class="sxs-lookup"><span data-stu-id="c6700-151">hello default value is ''.</span></span> [<span data-ttu-id="c6700-152">相關資訊</span><span class="sxs-lookup"><span data-stu-id="c6700-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="c6700-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="c6700-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="c6700-154">集合</span><span class="sxs-lookup"><span data-stu-id="c6700-154">Collection</span></span> |<span data-ttu-id="c6700-155">定義從哪些 toodownload hello WMF 的替代位置。</span><span class="sxs-lookup"><span data-stu-id="c6700-155">Defines alternate locations from which toodownload hello WMF.</span></span> [<span data-ttu-id="c6700-156">相關資訊</span><span class="sxs-lookup"><span data-stu-id="c6700-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="c6700-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c6700-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="c6700-158">集合</span><span class="sxs-lookup"><span data-stu-id="c6700-158">Collection</span></span> |<span data-ttu-id="c6700-159">定義您想要 toopass tooyour DSC 設定的所有參數。</span><span class="sxs-lookup"><span data-stu-id="c6700-159">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="c6700-160">這個屬性已加密。</span><span class="sxs-lookup"><span data-stu-id="c6700-160">This property is encrypted.</span></span> |
| <span data-ttu-id="c6700-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c6700-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="c6700-162">字串</span><span class="sxs-lookup"><span data-stu-id="c6700-162">string</span></span> |<span data-ttu-id="c6700-163">指定 hello SAS 權杖 tooaccess hello URL configuration.url 所定義。</span><span class="sxs-lookup"><span data-stu-id="c6700-163">Specifies hello SAS token tooaccess hello URL defined by configuration.url.</span></span> <span data-ttu-id="c6700-164">這個屬性已加密。</span><span class="sxs-lookup"><span data-stu-id="c6700-164">This property is encrypted.</span></span> |
| <span data-ttu-id="c6700-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c6700-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="c6700-166">字串</span><span class="sxs-lookup"><span data-stu-id="c6700-166">string</span></span> |<span data-ttu-id="c6700-167">指定 hello SAS 權杖 tooaccess hello URL configurationData.url 所定義。</span><span class="sxs-lookup"><span data-stu-id="c6700-167">Specifies hello SAS token tooaccess hello URL defined by configurationData.url.</span></span> <span data-ttu-id="c6700-168">這個屬性已加密。</span><span class="sxs-lookup"><span data-stu-id="c6700-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="c6700-169">Settings 與ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="c6700-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="c6700-170">所有的設定會儲存在設定文字檔 hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="c6700-170">All settings are saved in a settings text file on hello VM.</span></span>
<span data-ttu-id="c6700-171">在 [設定] 下的屬性是公用屬性，因為它們不會加密 hello 設定文字檔案中。</span><span class="sxs-lookup"><span data-stu-id="c6700-171">Properties under 'settings' are public properties because they are not encrypted in hello settings text file.</span></span>
<span data-ttu-id="c6700-172">'ProtectedSettings' 下的屬性已經使用憑證加密，並不會顯示以 hello VM 上的此檔案中的純文字。</span><span class="sxs-lookup"><span data-stu-id="c6700-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on hello VM.</span></span>

<span data-ttu-id="c6700-173">如果 hello 組態需要認證，因此可以包含在 protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="c6700-173">If hello configuration needs credentials, they can be included in protectedSettings:</span></span>

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

## <a name="example"></a><span data-ttu-id="c6700-174">範例</span><span class="sxs-lookup"><span data-stu-id="c6700-174">Example</span></span>
<span data-ttu-id="c6700-175">hello 以下範例衍生自 hello"Getting Started"區段 hello [DSC 延伸模組處理常式概觀 頁面](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c6700-175">hello following example derives from hello "Getting Started" section of hello [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="c6700-176">這個範例會使用資源管理員範本，而不是 cmdlet toodeploy hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="c6700-176">This example uses Resource Manager templates instead of cmdlets toodeploy hello extension.</span></span> <span data-ttu-id="c6700-177">儲存 hello"IisInstall.ps1 」 設定，請將它放在。ZIP 檔案，以及可存取的 URL 中的上傳 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6700-177">Save hello "IisInstall.ps1" configuration, place it in a .ZIP file, and upload hello file in an accessible URL.</span></span> <span data-ttu-id="c6700-178">這個範例會使用 Azure blob 儲存體，但可能 toodownload。從任意地點使用任意的 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6700-178">This example uses Azure blob storage, but it is possible toodownload .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="c6700-179">在 hello Azure Resource Manager 範本，hello 下列程式碼會指示 hello VM toodownload hello 正確的檔案並執行 hello 適當的 PowerShell 函式：</span><span class="sxs-lookup"><span data-stu-id="c6700-179">In hello Azure Resource Manager template, hello following code instructs hello VM toodownload hello correct file and run hello appropriate PowerShell function:</span></span>

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

## <a name="updating-from-hello-previous-format"></a><span data-ttu-id="c6700-180">從舊格式 hello 更新</span><span class="sxs-lookup"><span data-stu-id="c6700-180">Updating from hello Previous Format</span></span>
<span data-ttu-id="c6700-181">在 hello 舊格式 （包含 hello 公用屬性 ModulesUrl、 ConfigurationFunction、 SasToken 或屬性） 會自動調整 toohello 目前的格式，並如同之前所執行。</span><span class="sxs-lookup"><span data-stu-id="c6700-181">Any settings in hello previous format (containing hello public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt toohello current format and run just as they did before.</span></span>

<span data-ttu-id="c6700-182">下列結構描述的 hello 是何種 hello 先前設定的結構描述看起來像：</span><span class="sxs-lookup"><span data-stu-id="c6700-182">hello following schema is what hello previous settings schema looked like:</span></span>

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

<span data-ttu-id="c6700-183">以下是如何 hello 舊格式會調整 toohello 目前的格式：</span><span class="sxs-lookup"><span data-stu-id="c6700-183">Here's how hello previous format adapts toohello current format:</span></span>

| <span data-ttu-id="c6700-184">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c6700-184">Property Name</span></span> | <span data-ttu-id="c6700-185">先前結構描述對等項目</span><span class="sxs-lookup"><span data-stu-id="c6700-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="c6700-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="c6700-186">settings.wmfVersion</span></span> |<span data-ttu-id="c6700-187">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="c6700-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="c6700-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="c6700-188">settings.configuration.url</span></span> |<span data-ttu-id="c6700-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="c6700-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="c6700-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="c6700-190">settings.configuration.script</span></span> |<span data-ttu-id="c6700-191">settings.ConfigurationFunction 的第一個部分 ('\\\\' 之前)</span><span class="sxs-lookup"><span data-stu-id="c6700-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="c6700-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="c6700-192">settings.configuration.function</span></span> |<span data-ttu-id="c6700-193">settings.ConfigurationFunction 的第二個部分 ('\\\\' 之後)</span><span class="sxs-lookup"><span data-stu-id="c6700-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="c6700-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c6700-194">settings.configurationArguments</span></span> |<span data-ttu-id="c6700-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="c6700-195">settings.Properties</span></span> |
| <span data-ttu-id="c6700-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="c6700-196">settings.configurationData.url</span></span> |<span data-ttu-id="c6700-197">protectedSettings.DataBlobUri (不含 SAS 權杖)</span><span class="sxs-lookup"><span data-stu-id="c6700-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="c6700-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="c6700-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="c6700-199">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="c6700-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="c6700-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="c6700-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="c6700-201">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="c6700-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="c6700-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c6700-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="c6700-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="c6700-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="c6700-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c6700-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="c6700-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="c6700-205">settings.SasToken</span></span> |
| <span data-ttu-id="c6700-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c6700-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="c6700-207">SAS token from protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="c6700-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="c6700-208">疑難排解 - 錯誤碼 1100</span><span class="sxs-lookup"><span data-stu-id="c6700-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="c6700-209">錯誤代碼 1100 至指出有 hello 使用者輸入 toohello DSC 擴充功能有問題。</span><span class="sxs-lookup"><span data-stu-id="c6700-209">Error Code 1100 indicates that there is a problem with hello user input toohello DSC extension.</span></span>
<span data-ttu-id="c6700-210">這些錯誤的 hello 文字是變數，且可能會變更。</span><span class="sxs-lookup"><span data-stu-id="c6700-210">hello text of these errors is variable and may change.</span></span>
<span data-ttu-id="c6700-211">以下是一些您可能會碰到的 hello 錯誤和修正它們。</span><span class="sxs-lookup"><span data-stu-id="c6700-211">Here are some of hello errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="c6700-212">無效的值</span><span class="sxs-lookup"><span data-stu-id="c6700-212">Invalid Values</span></span>
<span data-ttu-id="c6700-213">「Privacy.dataCollection 為 '{0}'。</span><span class="sxs-lookup"><span data-stu-id="c6700-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="c6700-214">hello 只可能的值為 '、 'Enable' 和 'Disable'"「 WmfVersion 為 '{0}'。</span><span class="sxs-lookup"><span data-stu-id="c6700-214">hello only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="c6700-215">可能的值為 …</span><span class="sxs-lookup"><span data-stu-id="c6700-215">Only possible values are …</span></span> <span data-ttu-id="c6700-216">和 'latest'"</span><span class="sxs-lookup"><span data-stu-id="c6700-216">and 'latest'"</span></span>

<span data-ttu-id="c6700-217">問題︰不允許所提供的值。</span><span class="sxs-lookup"><span data-stu-id="c6700-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="c6700-218">解決方案： 變更 hello 有效值 tooa 有效的值。</span><span class="sxs-lookup"><span data-stu-id="c6700-218">Solution: Change hello invalid value tooa valid value.</span></span> <span data-ttu-id="c6700-219">請參閱 hello 詳細資料 區段中的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="c6700-219">See hello table in hello Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="c6700-220">無效的 URL</span><span class="sxs-lookup"><span data-stu-id="c6700-220">Invalid URL</span></span>
<span data-ttu-id="c6700-221">「ConfigurationData.url 為 '{0}'。</span><span class="sxs-lookup"><span data-stu-id="c6700-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="c6700-222">這不是有效的 URL」 「DataBlobUri 為 '{0}'。</span><span class="sxs-lookup"><span data-stu-id="c6700-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="c6700-223">這不是有效的 URL」 「Configuration.url 為 '{0}'。</span><span class="sxs-lookup"><span data-stu-id="c6700-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="c6700-224">這不是有效的 URL」</span><span class="sxs-lookup"><span data-stu-id="c6700-224">This is not a valid URL"</span></span>

<span data-ttu-id="c6700-225">問題︰所提供的 URL 無效。</span><span class="sxs-lookup"><span data-stu-id="c6700-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="c6700-226">解決方式︰檢查您提供的所有 URL。</span><span class="sxs-lookup"><span data-stu-id="c6700-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="c6700-227">請確定所有 Url 都解析 toovalid 位置 hello 延伸模組可以存取 hello 遠端電腦上。</span><span class="sxs-lookup"><span data-stu-id="c6700-227">Make sure all URLs resolve toovalid locations that hello extension can access on hello remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="c6700-228">無效的 ConfigurationArgument 類型</span><span class="sxs-lookup"><span data-stu-id="c6700-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="c6700-229">「無效的 configurationArguments 類型 {0}」</span><span class="sxs-lookup"><span data-stu-id="c6700-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="c6700-230">問題： hello ConfigurationArguments 屬性無法解析 tooa Hashtable 物件。</span><span class="sxs-lookup"><span data-stu-id="c6700-230">Problem: hello ConfigurationArguments property cannot resolve tooa Hashtable object.</span></span> 

<span data-ttu-id="c6700-231">解決方式︰讓 ConfigurationArguments 屬性變成雜湊表。</span><span class="sxs-lookup"><span data-stu-id="c6700-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="c6700-232">請遵循 hello hello 前面範例中所提供的格式。</span><span class="sxs-lookup"><span data-stu-id="c6700-232">Follow hello format provided in hello preceeding example.</span></span> <span data-ttu-id="c6700-233">請留意引號、逗號和括號。</span><span class="sxs-lookup"><span data-stu-id="c6700-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="c6700-234">重複的 ConfigurationArguments</span><span class="sxs-lookup"><span data-stu-id="c6700-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="c6700-235">「在公用和受保護的 configurationArguments 中找到重複的引數 '{0}'」</span><span class="sxs-lookup"><span data-stu-id="c6700-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="c6700-236">問題： hello ConfigurationArguments 公用的設定中，而且 hello ConfigurationArguments 受保護的設定中包含以 hello 屬性相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="c6700-236">Problem: hello ConfigurationArguments in public settings and hello ConfigurationArguments in protected settings contain properties with hello same name.</span></span>

<span data-ttu-id="c6700-237">解決方案： 移除其中一個 hello 重複的屬性。</span><span class="sxs-lookup"><span data-stu-id="c6700-237">Solution: Remove one of hello duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="c6700-238">遺漏的屬性</span><span class="sxs-lookup"><span data-stu-id="c6700-238">Missing Properties</span></span>
<span data-ttu-id="c6700-239">「Configuration.function 要求指定 configuration.url 或 configuration.module」</span><span class="sxs-lookup"><span data-stu-id="c6700-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="c6700-240">「Configuration.url 要求指定 configuration.script」</span><span class="sxs-lookup"><span data-stu-id="c6700-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="c6700-241">「Configuration.script 要求指定 configuration.url」</span><span class="sxs-lookup"><span data-stu-id="c6700-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="c6700-242">「Configuration.url 要求指定 configuration.function」</span><span class="sxs-lookup"><span data-stu-id="c6700-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="c6700-243">「ConfigurationUrlSasToken 要求指定 configuration.url」</span><span class="sxs-lookup"><span data-stu-id="c6700-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="c6700-244">「ConfigurationDataUrlSasToken 要求指定 configurationData.url」</span><span class="sxs-lookup"><span data-stu-id="c6700-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="c6700-245">問題︰定義的屬性需要另一個遺漏的屬性。</span><span class="sxs-lookup"><span data-stu-id="c6700-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="c6700-246">解決方式︰</span><span class="sxs-lookup"><span data-stu-id="c6700-246">Solutions:</span></span> 

* <span data-ttu-id="c6700-247">提供 hello 遺漏的屬性。</span><span class="sxs-lookup"><span data-stu-id="c6700-247">Provide hello missing property.</span></span>
* <span data-ttu-id="c6700-248">移除 hello 屬性需要 hello 遺漏的屬性。</span><span class="sxs-lookup"><span data-stu-id="c6700-248">Remove hello property that needs hello missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6700-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6700-249">Next Steps</span></span>
<span data-ttu-id="c6700-250">深入了解 DSC，以及虛擬機器規模集中[以 hello Azure DSC 延伸模組使用虛擬機器規模集](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="c6700-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with hello Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="c6700-251">如需詳細資料，請參閱 [DSC 的安全認證管理](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c6700-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c6700-252">如需有關 hello Azure DSC 延伸模組處理常式的詳細資訊，請參閱[簡介 toohello Azure Desired State Configuration 延伸模組處理常式](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c6700-252">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c6700-253">如需有關 PowerShell DSC[造訪 hello PowerShell 文件中心](https://msdn.microsoft.com/powershell/dsc/overview)。</span><span class="sxs-lookup"><span data-stu-id="c6700-253">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

