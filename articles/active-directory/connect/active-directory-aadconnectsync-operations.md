---
title: "Azure AD Connect 同步：作業工作和考量 | Microsoft Docs"
description: "本主題描述 Azure AD Connect 同步處理的操作工作以及 tooprepare 來操作此元件。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a>Azure AD Connect 同步處理：作業工作和考量
本主題的 hello 目標是 Azure AD Connect 同步處理的 toodescribe 操作工作。

## <a name="staging-mode"></a>預備模式
預備模式可以用於許多案例，包括：

* 高可用性。
* 測試和部署新的組態變更。
* 介紹新的伺服器，並解除委任 hello 舊。

具有預備模式中的伺服器，您可以變更變更 toohello 組態和預覽 hello 進行 hello 伺服器作用中。 它也可讓您 toorun 完整匯入和完整同步處理 tooverify 到生產環境的所有變更都會先進行這些變更。

在安裝期間，您可以選取在 hello 伺服器 toobe**預備模式**。 這個動作可 hello 伺服器作用中匯入和同步處理，但不會執行任何的匯出。 預備模式的伺服器不會執行密碼同步處理或密碼回寫，即使您在安裝期間選取這些功能也一樣。 當您停用預備模式時，hello 伺服器就會啟動匯出、 啟用密碼同步處理，並啟用密碼回寫。

您仍然可以使用 hello 同步處理服務管理員來強制執行匯出。

預備模式中的伺服器會繼續從 Active Directory 和 Azure AD 的 tooreceive 變更。 它永遠高於 hello 責任的另一部伺服器 hello 最新的變更，並可以非常快速採取的複本。 如果您進行組態變更 tooyour 主要伺服器，則責任 toomake hello 中預備模式的相同變更 toohello 伺服器。

對於了解的較舊的同步處理技術，預備模式的 hello 十分不同 hello 伺服器有它自己的 SQL 資料庫。 此架構可讓 hello 預備模式伺服器 toobe 位於不同的資料中心。

### <a name="verify-hello-configuration-of-a-server"></a>確認組態伺服器 hello
tooapply 這種方法，請遵循下列步驟：

1. [準備](#prepare)
2. [組態](#configuration)
3. [匯入和同步處理](#import-and-synchronize)
4. [Verify](#verify)
5. [切換作用中的伺服器](#switch-active-server)

#### <a name="prepare"></a>準備
1. 安裝 Azure AD Connect，請選取**預備模式**，並取消選取**啟動同步處理**hello hello 安裝精靈 中的最後一頁上。 此模式可讓您 toorun hello 同步處理引擎以手動方式。
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)
2. 符號登出/登入和 hello 從開始功能表中選取**同步處理服務**。

#### <a name="configuration"></a>組態
如果您進行了自訂變更 toohello 主要伺服器和想 toocompare hello 組態以 hello 臨時伺服器，然後使用[Azure AD Connect 設定文件產生器](https://github.com/Microsoft/AADConnectConfigDocumenter)。

#### <a name="import-and-synchronize"></a>匯入和同步處理
1. 選取**連接器**，並選取 hello 與 hello 類型的第一個連接器**Active Directory 網域服務**。 按一下 [執行]，選取 [完整匯入] 和 [確定]。 對這種類型的所有連接器執行下列動作。
2. 選取 hello 連接器類型**Azure Active Directory (Microsoft)**。 按一下 [執行]，選取 [完整匯入] 和 [確定]。
3. 請確定仍然選取連接器 hello 索引標籤。 針對每一個 [Active Directory Domain Services] 類型的連接器按一下 [執行]、選取 [差異同步處理] 和 [確定]。
4. 選取 hello 連接器類型**Azure Active Directory (Microsoft)**。 按一下 [執行]，選取 [差異同步處理] 和 [確定]。

您必須現在分段的匯出變更 tooAzure AD 和內部部署 AD （如果您使用 Exchange 混合部署）。 hello 接下來的步驟可讓您 tooinspect 什麼是關於 toochange 之前您在真正開始 hello 匯出 toohello 目錄。

#### <a name="verify"></a>驗證
1. 啟動 cmd 提示字元並移過`%ProgramFiles%\Microsoft Azure AD Sync\bin`
2. 執行： `csexport "Name of Connector" %temp%\export.xml /f:x` hello hello 連接器名稱可以在同步處理服務。 其名稱類似的 too"contoso.com – AAD"Azure ad。
3. 複製 hello PowerShell 指令碼從 hello 區段[CSAnalyzer](#appendix-csanalyzer) tooa 檔名為`csanalyzer.ps1`。
4. 開啟 PowerShell 視窗並瀏覽 toohello 資料夾建立 hello PowerShell 指令碼的位置。
5. 執行：`.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`。
6. 您現在已有一個可在 Microsoft Excel 中檢查的名為 **processedusers1.csv** 的檔案。 這個檔案中找到所有分段的變更匯出 toobe tooAzure AD。
7. 進行必要的變更 toohello 資料或組態，直到即將匯出的 toobe 的變更預期的 hello 執行這些步驟一次 （匯入和同步處理和驗證）。

#### <a name="switch-active-server"></a>切換作用中的伺服器
1. Hello 目前作用中伺服器上，讓它不會匯出 tooAzure AD 關閉 hello 伺服器 （DirSync/FIM/Azure AD 同步處理），或在預備模式 (Azure AD Connect) 進行設定。
2. 中的 hello 伺服器上執行 hello 安裝精靈**預備模式**和停用**預備模式**。
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)

## <a name="disaster-recovery"></a>災害復原
Hello 實作設計的一部分是針對哪些 toodo tooplan，以防萬一發生嚴重損壞您會遺失 hello 同步伺服器。 有不同的模型 toouse 和哪一個 toouse 取決於數個因素，包括：

* 什麼是不被可以讓您對於容錯 hello 停機期間的 Azure AD 中變更 tooobjects 嗎？
* 如果您使用密碼同步處理時，請勿 hello 使用者接受它們在 Azure AD 中有 toouse hello 舊密碼，如果他們變更它在內部部署嗎？
* 您是否對即時作業有相依性，例如密碼回寫？

根據 hello 答案 toothese 問題和貴組織的原則，其中一個 hello 下列策略可以實作：

* 必要時重建。
* 具有備用的待命伺服器，稱為「預備模式」 。
* 使用虛擬機器。

如果您不要使用 hello 內建 SQL Express 資料庫，則您也應該檢閱 hello [SQL 高可用性](#sql-high-availability)> 一節。

### <a name="rebuild-when-needed"></a>必要時重建
可行的策略是在伺服器重建時所需的 tooplan。 通常，安裝 hello 同步處理引擎及執行 hello 初始匯入，而且可以在幾小時的時間內完成同步處理。 如果沒有可用的備用的伺服器，則可能 tootemporarily 使用網域控制站 toohost hello 同步處理引擎。

hello 同步作業引擎伺服器不會儲存有關 hello 物件的任何狀態，因此可以重建 hello 資料庫，從 Active Directory 與 Azure AD 中的 hello 資料。 hello **sourceAnchor**屬性是使用的 toojoin hello 物件從內部部署和雲端的 hello。 如果您要重建 hello 與現有物件的伺服器內部部署且 hello 雲端，然後 hello 同步處理引擎比對一次上重新安裝這些物件。 hello toodocument，儲存事項 hello 設定的變更 toohello 伺服器，例如篩選和同步處理規則。 這些自訂設定必須在您開始同步處理之前重新套用。

### <a name="have-a-spare-standby-server---staging-mode"></a>具有備用的待命伺服器 - 預備模式
如果您有更複雜的環境，則建議使用一或多個待命伺服器。 在安裝期間，您可以啟用在伺服器 toobe**預備模式**。

如需詳細資訊，請參閱[預備模式](#staging-mode)。

### <a name="use-virtual-machines"></a>使用虛擬機器
一般和受支援的方法是在虛擬機器的 toorun hello 同步處理引擎。 萬一 hello 主機有問題，與 hello 同步作業引擎伺服器 hello 映像可以是移轉的 tooanother 伺服器。

### <a name="sql-high-availability"></a>SQL 高可用性
如果您不使用 SQL Server Express 隨附於 Azure AD Connect 的 hello，然後 SQL Server 的高可用性也必須考量。 支援的 hello 高可用性解決方案包含 SQL 叢集和 AOA （Alwayson 可用性群組）。 不支援的解決方案包括鏡像。

已加入支援 SQL AOA tooAzure AD 1.1.524.0 版本中的連接。 您必須在安裝 Azure AD Connect 之前啟用 SQL AOA。 在安裝期間，Azure AD Connect 會偵測是否提供 hello SQL 執行個體已啟用 SQL AOA 與否。 如果已啟用 SQL AOA，Azure AD Connect 進一步找出 SQL AOA 是否設定的 toouse 同步或非同步複寫。 當設定 hello 可用性群組接聽程式，建議您設定 hello RegisterAllProvidersIP 屬性 too0。 這是因為 Azure AD Connect 目前使用 SQL Native Client tooconnect tooSQL 和 SQL Native Client 不支援使用 MultiSubNetFailover 屬性 hello。

## <a name="appendix-csanalyzer"></a>附錄 CSAnalyzer
請參閱 hello 節[確認](#verify)如何 toouse 此指令碼。

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a>後續步驟
**概觀主題**  

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)  
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)  
