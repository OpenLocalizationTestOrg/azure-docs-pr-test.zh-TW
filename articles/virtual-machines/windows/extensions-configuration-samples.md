---
title: "Windows VM 延伸模組的範例組態 | Microsoft Docs"
description: "編寫延伸模組與範本的範例組態"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a1cee6c-51ea-4c03-b607-f158586d7175
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: a22962690854d273377f7295ab5dd49419f5a354
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-windows-vm-extension-configuration-samples"></a><span data-ttu-id="800ab-103">Azure Windows VM 延伸模組組態範例</span><span class="sxs-lookup"><span data-stu-id="800ab-103">Azure Windows VM Extension Configuration Samples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="800ab-104">PowerShell - 範本</span><span class="sxs-lookup"><span data-stu-id="800ab-104">PowerShell - Template</span></span>](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> * [<span data-ttu-id="800ab-105">CLI - 範本</span><span class="sxs-lookup"><span data-stu-id="800ab-105">CLI - Template</span></span>](../linux/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="800ab-106">本文提供範例組態，可用來設定 Windows VM 的 Azure VM 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="800ab-106">This article provides sample configuration for configuring Azure VM Extensions for Windows VMs.</span></span>

<span data-ttu-id="800ab-107">若要深入了解這些延伸模組，請參閱 [Azure VM 延伸模組概觀](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="800ab-107">To learn more about these extensions, see [Azure VM Extensions Overview.](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="800ab-108">若要深入了解如何撰寫延伸模組範本，請參閱 [撰寫延伸模組範本](extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="800ab-108">To learn more about authoring extension templates, see [Authoring Extension Templates.](extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="800ab-109">本文列出部分 Windows 延伸模組所需的組態值。</span><span class="sxs-lookup"><span data-stu-id="800ab-109">This article lists expected configuration values for some of the Windows Extensions.</span></span>

## <a name="sample-template-snippet-for-vm-extensions-with-iaas-vms"></a><span data-ttu-id="800ab-110">VM 擴充功能與 IaaS VM 的範例範本程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="800ab-110">Sample template snippet for VM Extensions with IaaS VMs.</span></span>
<span data-ttu-id="800ab-111">用於部署延伸模組的範本程式碼片段如下所示：</span><span class="sxs-lookup"><span data-stu-id="800ab-111">The template snippet for Deploying extensions looks as following:</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "autoUpgradeMinorVersion":true,
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

## <a name="sample-template-snippet-for-vm-extensions-with-vm-scale-sets"></a><span data-ttu-id="800ab-112">VM 擴充功能與 VM 調整集的範例範本程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="800ab-112">Sample template snippet for VM Extensions with VM Scale Sets.</span></span>
    {
     "type":"Microsoft.Compute/virtualMachineScaleSets",
    ....
           "extensionProfile":{
           "extensions":[
             {
               "name":"extension Name",
               "properties":{
                 "publisher":"Publisher Namespace",
                 "type":"extension Name",
                 "typeHandlerVersion":"extension version",
                 "autoUpgradeMinorVersion":true,
                 "settings":{
                 // Extension specific configuration goes in here.
                 }
               }
              }
            }
          }

<span data-ttu-id="800ab-113">部署延伸模組之前，請檢查最新的延伸模組版本，並以目前最新版本取代 "typeHandlerVersion"。</span><span class="sxs-lookup"><span data-stu-id="800ab-113">Before deploying the extension please check the latest extension version and replace the "typeHandlerVersion" with the current latest version.</span></span>

<span data-ttu-id="800ab-114">本文其餘部分提供 Windows VM 延伸模組的範例組態。</span><span class="sxs-lookup"><span data-stu-id="800ab-114">Rest of the article provides sample configurations for Windows VM Extensions.</span></span>

<span data-ttu-id="800ab-115">部署延伸模組之前，請檢查最新的延伸模組版本，並以目前最新版本取代 "typeHandlerVersion"。</span><span class="sxs-lookup"><span data-stu-id="800ab-115">Before deploying the extension please check the latest extension version and replace the "typeHandlerVersion" with the current latest version.</span></span>

### <a name="customscript-extension-14"></a><span data-ttu-id="800ab-116">CustomScript 擴充功能 1.4。</span><span class="sxs-lookup"><span data-stu-id="800ab-116">CustomScript Extension 1.4.</span></span>
      {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.4",
          "settings": {
              "fileUris": [
                  "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
              ],
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
          },
          "protectedSettings": {
            "storageAccountName": "yourStorageAccountName",
            "storageAccountKey": "yourStorageAccountKey"
          }
      }

#### <a name="parameter-description"></a><span data-ttu-id="800ab-117">參數說明︰</span><span class="sxs-lookup"><span data-stu-id="800ab-117">Parameter description:</span></span>
* <span data-ttu-id="800ab-118">fileUris︰擴充功能將在 VM 上下載之檔案的 URL 清單 (以逗號分隔)。</span><span class="sxs-lookup"><span data-stu-id="800ab-118">fileUris : Comma seperated list of urls of the files that will be downloaded on the VM by the Extension.</span></span> <span data-ttu-id="800ab-119">如果未指定，則不會下載任何檔案。</span><span class="sxs-lookup"><span data-stu-id="800ab-119">No files are downloaded if nothing is specified.</span></span> <span data-ttu-id="800ab-120">如果檔案是在 Azure 儲存體中，則可以將 fileURLs 標示為私用，而且對應的 storageAccountName 和 storageAccountKey 可以傳遞為私用參數來存取這些檔案。</span><span class="sxs-lookup"><span data-stu-id="800ab-120">If the files are in Azure Storage, the fileURLs can be marked private and the correspoding storageAccountName and storageAccountKey can be passed as private parameters to access these files.</span></span>
* <span data-ttu-id="800ab-121">commandToExecute：[必要參數]：這是擴充功能將執行的命令。</span><span class="sxs-lookup"><span data-stu-id="800ab-121">commandToExecute : [Mandatory Parameter] : This is the command that will be executed by the Extension.</span></span>
* <span data-ttu-id="800ab-122">storageAccountName：[選用參數]：用於存取 fileURLs (如果標示為私用) 的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="800ab-122">storageAccountName : [Optional Parameter] : Storage Account Name for accessing the fileURLs, if they are marked as private.</span></span>
* <span data-ttu-id="800ab-123">storageAccountKey：[選用參數]：用於存取 fileURLs (如果標示為私用) 的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="800ab-123">storageAccountKey : [Optional Parameter] : Storage Account Key for accessing the fileURLs, if they are marked as private.</span></span>

### <a name="customscript-extension-17"></a><span data-ttu-id="800ab-124">CustomScript 擴充功能 1.7。</span><span class="sxs-lookup"><span data-stu-id="800ab-124">CustomScript Extension 1.7.</span></span>
<span data-ttu-id="800ab-125">請參閱 CustomScript 1.4 版的參數說明。</span><span class="sxs-lookup"><span data-stu-id="800ab-125">Please refer to CustomScript version 1.4 for parameter description.</span></span> <span data-ttu-id="800ab-126">1.7 版支援將指令碼參數 (commandToExecute) 傳送為 protectedSettings，在此情況下，它們會在傳送之前進行加密。</span><span class="sxs-lookup"><span data-stu-id="800ab-126">Version 1.7 introduces support for sending script parameters(commandToExecute) as protectedSettings, in which case they will be encrypted before sending.</span></span> <span data-ttu-id="800ab-127">'commandToExecute' 參數可以指定於 settings 或 protectedSettings，但不能同時指定於兩者。</span><span class="sxs-lookup"><span data-stu-id="800ab-127">'commandToExecute' parameter can be specified either in settings or protectedSettings but not in both.</span></span>

        {
            "publisher": "Microsoft.Compute",
            "type": "CustomScriptExtension",
            "typeHandlerVersion": "1.7",
            "settings": {
                "fileUris": [
                    "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
                ],
                "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
            },
            "protectedSettings": {
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1",
              "storageAccountName": "yourStorageAccountName",
              "storageAccountKey": "yourStorageAccountKey"
            }
        }

### <a name="vmaccess-extension"></a><span data-ttu-id="800ab-128">VMAccess 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="800ab-128">VMAccess Extension.</span></span>
      {
          "publisher": "Microsoft.Compute",
          "type": "VMAccessAgent",
          "typeHandlerVersion": "2.0",
          "settings": {
            "UserName" : "New User Name"
          },
          "protectedSettings": {
            "Password" : "New Password"
          }
      }

### <a name="dsc-extension"></a><span data-ttu-id="800ab-129">DSC 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="800ab-129">DSC Extension.</span></span>
      {
          "publisher": "Microsoft.Powershell",
          "type": "DSC",
          "typeHandlerVersion": "2.1(Recommendation is to use the latest version)",
          "settings": {
              "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
              "SasToken": "Optional : SAS Token if ModulesUrl points to Azure Blob Storage",
              "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
              "Properties": {
                  "ParameterToConfigurationFunction1": "Value1",
                  "ParameterToConfigurationFunction2": "Value2",
                  "ParameterOfTypePSCredential1": {
                      "UserName": "UsernameValue1",
                      "Password": "PrivateSettingsRef:Key1(Value is a reference to a member of the Items object in the protected settings)"
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
              "DataBlobUri": "optional : https: //UrlToConfigurationData.psd1"
          }
      }


### <a name="symantec-endpoint-protection"></a><span data-ttu-id="800ab-130">Symantec Endpoint Protection。</span><span class="sxs-lookup"><span data-stu-id="800ab-130">Symantec Endpoint Protection.</span></span>
      {
        "publisher": "SymantecEndpointProtection",
        "type": "Symantec",
        "typeHandlerVersion": "12.1",
        "settings": {}
      }

### <a name="trend-micro-deep-security-agent"></a><span data-ttu-id="800ab-131">Trend Micro Deep Security Agent。</span><span class="sxs-lookup"><span data-stu-id="800ab-131">Trend Micro Deep Security Agent.</span></span>
      {
        "publisher": "TrendMicro.DeepSecurity",
        "type": "TrendMicroDSA",
        "typeHandlerVersion": "9.6",
        "settings": {
          "ManagerAddress" : "Enter the externally accessible DNS name or IP address of the Deep Security Manager. Please enter \"agents.deepsecurity.trendmicro.com\" if using Deep Security as a Service",

          "ActivationPort" : "Enter the port number of the Deep Security Manager, default value - 443",

          "TenantIdentifier" : "Enter the tenant ID, which is a hyphenated, 36-character string available in the Deployment Scripts dialog box in the Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "TenantActivationPassword" : "Enter the tenant activation password, which is a hyphenated, 36-character string available in the Deployment Scripts dialog box in the Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "SecurityPolicy" : "Optional : Enter the name or numeric ID of the security policy defined in the Deep Security Manager which will be applied on agent activation to protect this virtual machine (recommended). No security policy will be applied to the virtual machine if this parameter is blank. This parameter is optional if using Deep Security as a Service."
        }
      }

### <a name="vormertric-transparent-encryption-agent"></a><span data-ttu-id="800ab-132">Vormertric Transparent Encryption Agent。</span><span class="sxs-lookup"><span data-stu-id="800ab-132">Vormertric Transparent Encryption Agent.</span></span>
            {
              "publisher": "Vormetric",
              "type": "VormetricTransparentEncryptionAgent",
              "typeHandlerVersion": "5.2",
              "settings": {
              }
            }

### <a name="puppet-enterprise-agent"></a><span data-ttu-id="800ab-133">Puppet Enterprise Agent。</span><span class="sxs-lookup"><span data-stu-id="800ab-133">Puppet Enterprise Agent.</span></span>
            {
              "publisher": "PuppetLabs",
              "type": "PuppetEnterpriseAgent",
              "typeHandlerVersion": "3.2",
              "settings": {
                "puppet_master_server" : "Puppet Master Server Name"
              }
            }  

### <a name="microsoft-monitoring-agent-for-azure-operational-insights"></a><span data-ttu-id="800ab-134">Microsoft Monitoring Agent for Azure Operational Insights</span><span class="sxs-lookup"><span data-stu-id="800ab-134">Microsoft Monitoring Agent for Azure Operational Insights</span></span>
            {
              "publisher": "Microsoft.EnterpriseCloud.Monitoring",
              "type": "MicrosoftMonitoringAgent",
              "typeHandlerVersion": "1.0",
              "settings": {
                "workspaceId" : "The Workspace ID is available from within the Direct Agent Configuration section of the Azure Operational Insights portal"
              }
              "protectedSettings": {
                "workspaceKey"  : "The Workspace Key is a string that is available from within the Direct Agent Configuration section of the Azure Operational Insights portal"
              }
              }
            }

### <a name="mcafee-endpointsecurity"></a><span data-ttu-id="800ab-135">McAfee EndpointSecurity</span><span class="sxs-lookup"><span data-stu-id="800ab-135">McAfee EndpointSecurity</span></span>
            {
              "publisher": "McAfee.EndpointSecurity",
              "type": "McAfeeEndpointSecurity",
              "typeHandlerVersion": "6.0",
              "settings": {
                "entitlementKey" : "Optional : Enter a valid entitlement key or leave blank for trial version",
                "featureVS"      : "Choose whether or not to install the Virus and Spyware Protection features : true|false",
                "featureBP"      : "Choose whether or not to install the Browser Protection feature : true|false",
                "featureFW"      : "Choose whether or not to install the Firewall Protection feature :true|false",
                "relayServer"    : "Allows VMs on the local subnet to receive updates through this VM when they are not connected to the internet : true|false"
              }
            }

### <a name="azure-iaas-antimalware"></a><span data-ttu-id="800ab-136">Azure IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="800ab-136">Azure IaaS Antimalware</span></span>
          {
            "publisher": "Microsoft.Azure.Security",
            "type": "IaaSAntimalware",
            "typeHandlerVersion": "1.2",
            "settings": {
              "AntimalwareEnabled": "true",
              "ExclusionsPaths"        : "Optional : ExclusionsPaths",
              "ExclusionsExtensions"   : "Optional : ExclusionsExtensions",
              "ExclusionsProcesses"   : "Optional : ExclusionsProcesses",
              "RealtimeProtectionEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsIsEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsScanType"   : "Optional : Quick|Full",
              "ScheduledScanSettingsDay"   : "Optional : Sunday-Saturday",
              "ScheduledScanSettingsTime"   : "Optional : When to perform the scheduled scan, measured in minutes from midnight,0-1440"
            }
          }

### <a name="eset-file-security"></a><span data-ttu-id="800ab-137">ESET File Security</span><span class="sxs-lookup"><span data-stu-id="800ab-137">ESET File Security</span></span>
          {
            "publisher": "ESET",
            "type": "FileSecurity",
            "typeHandlerVersion": "6.0",
            "settings": {
            }
          }

### <a name="datadog-agent"></a><span data-ttu-id="800ab-138">Datadog Agent</span><span class="sxs-lookup"><span data-stu-id="800ab-138">Datadog Agent</span></span>
          {
            "publisher": "Datadog.Agent",
            "type": "DatadogWindowsAgent",
            "typeHandlerVersion": "0.5",
            "settings": {
              "api_key" : "API Key from https://app.datadoghq.com/account/settings#api"
            }
          }

### <a name="confer-advanced-threat-prevention-and-incident-response-for-azure"></a><span data-ttu-id="800ab-139">Azure 適用的 Confer 進階威脅防禦及事件回應</span><span class="sxs-lookup"><span data-stu-id="800ab-139">Confer Advanced Threat Prevention and Incident Response for Azure</span></span>
          {
            "publisher": "Confer",
            "type": "ConferForAzure",
            "typeHandlerVersion": "1.0",
            "settings": {
              "ConferRegisterCode" : "Optional : Valid product registration code or leave it blank to register later",
              "ConferRegisterCode" : "Enter a valid server name if your account requires a dedicated confer backend server or leave it blank"
            }
          }

### <a name="cloudlink-securevm-agent"></a><span data-ttu-id="800ab-140">CloudLink SecureVM Agent</span><span class="sxs-lookup"><span data-stu-id="800ab-140">CloudLink SecureVM Agent</span></span>
          {
            "publisher": "CloudLinkEMC.SecureVM",
            "type": "CloudLinkSecureVMWindowsAgent",
            "typeHandlerVersion": "4.0",
            "settings": {
              "CloudLinkCenter" : "specify valid IP/FQDN to CloudLinkCenter"
            }
          }

### <a name="barracuda-vpn-connectivity-agent-for-microsoft-azure"></a><span data-ttu-id="800ab-141">Microsoft Azure 的 Barracuda VPN 連線代理程式</span><span class="sxs-lookup"><span data-stu-id="800ab-141">Barracuda VPN Connectivity Agent for Microsoft Azure</span></span>
          {
            "publisher": "Barracuda.Azure.ConnectivityAgent",
            "type": "BarracudaConnectivityAgent",
            "typeHandlerVersion": "3.5",
            "settings": {
              "ServerAddress" : "Host name or IP address of the VPN server - AES, AES256, Blowfish,CAST,DES,3DES,None",
              "EncryptionAlgorithm" : "Algorithm used to encrypt VPN traffic - MD5,SHA1,SHA256,None",
              "PKCS12File" : "Url for file containing certificate and private key used to authenticate against the VPN server",
              "PKCS12FilePassword" : "Password for the file containing certificate and private key"
            }
          }

### <a name="alert-logic-log-manager"></a><span data-ttu-id="800ab-142">Alert Logic Log Manager</span><span class="sxs-lookup"><span data-stu-id="800ab-142">Alert Logic Log Manager</span></span>
          {
            "publisher": "AlertLogic.Extension",
            "type": "AlertLogicLM",
            "typeHandlerVersion": "1.9",
            "settings": {
              "registrationKey" : " Alert Logic Log Manager registration key"
            }
          }

### <a name="chef-agent"></a><span data-ttu-id="800ab-143">Chef Agent</span><span class="sxs-lookup"><span data-stu-id="800ab-143">Chef Agent</span></span>
          {
            "publisher": "Chef.Bootstrap.WindowsAzure",
            "type": "ChefClient",
            "typeHandlerVersion": "1210.12",
            "settings": {
              "validation_key" : " Validation key",
              "client_rb" : "client_rb file",
              "runlist" : "Optional runlist"
            }
          }

### <a name="azure-diagnostics"></a><span data-ttu-id="800ab-144">Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="800ab-144">Azure Diagnostics</span></span>
<span data-ttu-id="800ab-145">如需有關如何設定診斷功能的詳細資訊，請參閱 [Azure 診斷延伸模組](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="800ab-145">For more details about how to configure diagnostics, see [Azure Diagnostics Extension](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

          {
            "publisher": "Microsoft.Azure.Diagnostics",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "1.5",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "xmlCfg": "[base64(variables('wadcfgx'))]",
              "storageAccount": "[parameters('diagnosticsStorageAccount')]"
            },
            "protectedSettings": {
            "storageAccountName": "[parameters('diagnosticsStorageAccount')]",
            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
            "storageAccountEndPoint": "https://core.windows.net"
          }
          }

### <a name="octopus-deploy-tentacle-agent"></a><span data-ttu-id="800ab-146">Octopus Deploy Tentacle 代理程式</span><span class="sxs-lookup"><span data-stu-id="800ab-146">Octopus Deploy Tentacle Agent</span></span>

<span data-ttu-id="800ab-147">如需有關如何在 Azure 上設定 Octopus Deploy Tentacle 的詳細資訊，請參閱 [Octopus 文件](https://octopus.com/docs/installation/installing-tentacles/azure-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="800ab-147">For more details about how to configure the Octopus Deploy Tentacle on Azure, see the [Octopus Documentation](https://octopus.com/docs/installation/installing-tentacles/azure-virtual-machines).</span></span>

          {
            "publisher": "OctopusDeploy.Tentacle",
            "type": "OctopusDeployWindowsTentacle",
            "typeHandlerVersion": "2.0",
            "autoUpgradeMinorVersion": "true",
            "settings": {
              "OctopusServerUrl": "(string, required) The url to the Octopus server portal.",
              "Environments": [ "(array of strings, required) The environments to which the Tentacle should be added." ],
              "Roles": [ "(array of strings, required) The roles to assign to the Tentacle." ],
              "CommunicationMode": "(string, required) Whether the Tentacle should wait for connections from the server ('Listen') or should poll the server ('Poll').",
              "Port": (int, required) The port to listen on for connections from the server (in 'Listen' mode), or the port on which to connect to the Octopus server ('Poll' mode).,
              "PublicHostNameConfiguration": "(string, optional) If in listening mode, how the server should contact the Tentacle. Can be 'PublicIP', 'FQDN', 'ComputerName' or 'Custom'. Defaults to 'PublicIp'.",
              "CustomPublicHostName": "(string, optional) If in listening mode, and 'PublicHostNameConfiguration' is set to 'Custom', the address that the server should use for this Tentacle.",
              "MachinePolicy": "(string, optional) The Machine Policy to assign to the Tentacle. If not specified, uses the default Machine Policy.",
              "Tenants": [ "(array of strings, optional) The tenants to assign to the Tentacle. The tenants feature must be enabled on the Octopus Server." ],
              "TenantTags": [ "(array of strings, optional) The tenant tags to assign to the Tentacle, in the format 'TagSet/TagName'. The tenants feature must be enabled on the Octopus Server." ]
            },
            "protectedSettings": {
              "ApiKey": "(string, required) The Api Key to use to connect to the Octopus server."
            }
          }

<span data-ttu-id="800ab-148">在上述範例中，請將版本號碼取代成最新的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="800ab-148">In the examples above, replace the version number with the latest version number.</span></span>

<span data-ttu-id="800ab-149">以下是使用自訂指令碼延伸模組的完整 VM 範本範例。</span><span class="sxs-lookup"><span data-stu-id="800ab-149">Here is an example of a full VM template with Custom Script Extension.</span></span>

[<span data-ttu-id="800ab-150">Windows VM 上的自訂指令碼延伸模組</span><span class="sxs-lookup"><span data-stu-id="800ab-150">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)
