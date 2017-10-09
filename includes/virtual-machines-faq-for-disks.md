# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>關於 Azure IaaS VM 磁碟及受控和非受控進階磁碟的常見問題集

此文章將回答有關 Azure 受控磁碟和 Azure 進階儲存體的一些常見問題。

## <a name="managed-disks"></a>受控磁碟

**何謂 Azure 受控磁碟？**

受控磁碟是可以為您管理儲存體帳戶而簡化 Azure IaaS VM 磁碟管理的一項功能。 如需詳細資訊，請參閱 hello[管理磁碟概觀](../articles/virtual-machines/windows/managed-disks-overview.md)。

**如果我從現有的 VHD (大小為 80 GB) 建立標準受控磁碟，需要多少費用？**

80 GB VHD 從建立標準受管理的磁碟視為與 hello 下一個可用的標準磁碟大小，也就是 S10 磁碟相同。 相應 toohello S10 磁碟價格收費。 如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。

**標準受控磁碟有任何交易成本嗎？**

是。 我們會根據每一筆交易向您收費。 如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。

**標準的受管理磁碟要收費 hello hello hello 磁碟資料的實際大小或佈建的 hello hello 磁碟容量？**

收費根據佈建的 hello hello 磁碟容量。 如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。

**進階受控磁碟和非受控磁碟的價格有何不同？**

hello 定價的受管理的高階磁碟是 hello 與未受管理的高階磁碟相同。

**可以變更 hello 儲存體帳戶類型 （Standard 或 Premium） 的 我的受管理磁碟嗎？**

是。 您可以使用 hello Azure 入口網站、 PowerShell 或 hello Azure CLI 變更 hello 儲存體帳戶類型的受管理的磁碟。

**有我可以複製或匯出受管理的磁碟 tooa 私人儲存體帳戶的方法嗎？**

是。 您可以使用 hello Azure 入口網站、 PowerShell 或 hello Azure CLI 匯出受管理的磁碟。

**可以使用 Azure 儲存體帳戶 toocreate 受管理磁碟的 VHD 檔案與不同的訂用帳戶嗎？**

否。

**可以使用 Azure 儲存體帳戶 toocreate 受管理磁碟的 VHD 檔案位於不同的區域嗎？**

否。

**客戶使用受控磁碟時是否有任何規模限制？**

受管理的磁碟排除 hello 限制與儲存體帳戶相關聯。 不過，每個訂閱受管理的磁碟的 hello 數目為有限的 too2，根據預設 000。 您可以呼叫支援 tooincrease 這個數字。

**我是否可以建立受控磁碟的增量快照集？**

否。 hello 目前的快照集功能可讓受管理磁碟的完整複本。 不過，我們正計劃在未來的 hello toosupport 增量快照。

**可用性設定組中的 VM 是否可以由受控和非受控磁碟混合組成？**

否。 所有受管理的磁碟或未受管理的所有磁碟，必須使用可用性設定組中的 hello Vm。 當您建立可用性設定組時，您可以選擇哪一種磁碟想 toouse。

**管理磁碟 hello 預設選項處於 hello Azure 入口網站？**

目前不可以，但是它會變成 hello 預設，在未來的 hello。

**我是否可以建立空的受控磁碟？**

是。 您可以建立空的磁碟。 受管理的磁碟可以建立獨立 VM，比方說，而不用附加它 tooa VM。

**什麼是支援的 hello 容錯網域計數的可用性設定組來使用受管理磁碟？**

依據 hello hello 可用性設定組來使用受管理磁碟所在的地區，hello 支援容錯網域計數是 2 或 3。

**如何為 hello 診斷設定的標準儲存體帳戶？**

您需要為 VM 診斷設定私人儲存體帳戶。 我們計劃在未來的 hello，tooswitch 診斷也 tooManaged 磁碟。

**受控磁碟適用何種角色型存取控制支援？**

受控磁碟支援三個主要預設角色︰

* 擁有者：可以管理所有項目，包括存取
* 參與者：可以管理存取以外的所有項目
* 讀取者：可以檢視所有項目，但是無法進行變更

**有我可以複製或匯出受管理的磁碟 tooa 私人儲存體帳戶的方法嗎？**

您可以取得 toocopy hello 內容 tooa 私用儲存體帳戶或內部部署儲存體的唯讀共用的存取簽章 URI hello 管理磁碟，並使用它。

**我是否可以建立受控磁碟的複本？**

客戶可以擷取受管理的磁碟的快照，然後再使用 hello 快照 toocreate 受管理的另一個磁碟。

**是否仍然支援非受控磁碟？**

是。 我們支援受控磁碟和非受控磁碟。 我們建議您針對新的工作負載使用受管理的磁碟，並移轉您目前的工作負載 toomanaged 磁碟。


**如果我建立 128 GB 的磁碟，然後再增加 hello 大小 too130 GB，將我支付 hello 下一個磁碟的大小 (512 GB)？**

是。

**我是否可以建立本地備援儲存體、異地備援儲存體和區域備援儲存體受控磁碟？**

Azure 受控磁碟目前只支援本地備援儲存體受控磁碟。

**我是否可以壓縮受控磁碟或縮減其大小？**

否。 目前不受支援此功能。 

**當特殊的 （不使用 hello 系統準備工具所建立或一般化） 操作系統磁碟使用的 tooprovision VM 可以變更 hello 電腦 name 屬性嗎？**

否。 您無法更新 hello 電腦名稱 屬性。 hello 新的 VM 會繼承它 hello 父 VM，這是使用的 toocreate hello 作業系統磁碟。 

**哪裡可以找到範例 Azure Resource Manager 範本 toocreate 與受管理磁碟 Vm？**
* [使用受控磁碟的範本清單](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

## <a name="managed-disks-and-storage-service-encryption"></a>受控磁碟和儲存體服務加密 

**當我建立受控磁碟時，依預設是否啟用 Azure 儲存體服務加密？**

是。

**使用者管理 hello 加密金鑰？**

Microsoft 會管理 hello 加密金鑰。

**我是否可以停用受控磁碟的儲存體服務加密？**

否。

**儲存體服務加密是否僅供特定地區使用？**

否。 它提供了管理磁碟可使用的所有 hello 區域。 受控磁碟在所有公開區域和德國都有提供。

**如何查看我的受控磁碟是否加密？**

您可以找出 hello hello Azure 入口網站、 hello Azure CLI 和 PowerShell 從受管理的磁碟建立時的時間。 如果 hello 時間之後 2017 年 6 月 9，便會加密您的磁碟。 

**如何加密我在 2017 年 6 月 10 日之前建立的現有磁碟？**

自 2017 年 6 月 10 寫入 tooexisting 管理磁碟的新資料會自動加密。 我們也想要規劃 tooencrypt 現有的資料，並在 hello 背景中將會以非同步方式發生 hello 加密。 如果您現在必須加密現有資料，請建立一份磁碟複本。 新的磁碟將會加密。

* [使用 Azure CLI hello 複製受管理的磁碟](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [使用 PowerShell 複製受控磁碟](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

**受管理的快照集和映像是否加密？**

是。 2017 年 6 月 9 日後建立之所有受管理的快照集和映像都將自動加密。 

**可以轉換 Vm 與位於儲存體帳戶，或已 toomanaged 先前加密的磁碟的 unmanaged 磁碟嗎？**

是

**從受控磁碟或快照集匯出的 VHD 是否也會加密？**

否。 但如果您匯出 VHD tooan 加密的加密受管理的磁碟或快照集，儲存體帳戶，然後它會加密。 

## <a name="premium-disks-managed-and-unmanaged"></a>進階磁碟：受控和非受控

**如果 VM 使用的大小系列支援進階儲存體，例如 DSv2，我是否可以同時連結進階和標準資料磁碟？** 

是。

**可以附加 premium 和 standard 磁碟 tooa 大小之資料數列不支援進階儲存體，例如 D、 Dv2、 G 或 F 數列嗎？**

否。 您可以附加只標準資料磁碟 tooVMs 針對未使用支援進階儲存體大小數列。

**如果我從現有的 VHD (大小為 80 GB) 建立進階資料磁碟，需要多少費用？**

80 GB VHD 從建立高階資料磁碟會被視為 hello 下一個可用的 premium 磁碟大小，也就是 P10 磁碟。 相應 toohello P10 磁碟價格收費。

**是否有交易成本 toouse 高階儲存體？**

依 IOPS 和輸送量的特定限制而佈建的每個磁碟大小，都有固定成本。 hello 其他成本包含傳出的頻寬和快照集的容量，如果適用的話。 如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。

**IOPS 及輸送量我可以從 hello 磁碟快取中取得的 hello 限制有哪些？**

hello 結合的限制快取和本機 SSD DS 系列的每個核心的 4,000 IOPS 和每個核心每秒的 33 MB。 hello GS 系列提供每個核心 5,000 IOPS 和每個核心每秒 50 MB。

**為的 hello 本機 SSD 支援受管理磁碟 VM？**

hello 本機 SSD 是隨附於受管理磁碟 VM 的暫存位置。 暫時儲存體不需額外的成本。 我們建議您不要使用此本機 SSD toostore 應用程式資料不是保存在 Azure Blob 儲存體。

**會那里任何影響 hello 的空白位置修剪上使用高階磁碟嗎？**

Azure 磁碟上是高階或標準磁碟上的空白位置修剪沒有缺點 toohello 使用了。

## <a name="new-disk-sizes-managed-and-unmanaged"></a>新磁碟大小：受控和非受控

**Hello 支援作業系統和資料磁碟最大磁碟大小為何？**

Azure 支援的作業系統磁碟的 hello 磁碟分割類型為 hello 主開機記錄 (MBR)。 hello MBR 格式支援向上 too2 TB 的磁碟大小。 hello Azure 支援的作業系統磁碟的最大大小為 2 TB。 Azure 支援 too4 TB 的資料磁碟上。 

**支援的 hello 最大頁面 blob 大小為何？**

Azure 支援的 hello 最大分頁 blob 大小為 8 TB (8,191 GB)。 我們不支援大於 4 TB (4095 GB) 附加 tooa VM 做為作業系統磁碟或資料的分頁 blob。

**我需要 toouse 新版本的 Azure tools toocreate 附加、 調整大小，並上傳大於 1 TB 的磁碟嗎？**

您不需要 tooupgrade 現有的 Azure tools toocreate、 附加，或調整大小大於 1 TB 的磁碟。 您的 VHD 檔案從 tooupload 內部直接 tooAzure 做為分頁 blob 或未受管理的磁碟，您需要 toouse hello 最新工具組：

|Azure 工具      | 支援的版本                                |
|-----------------|---------------------------------------------------|
|Azure PowerShell | 版本號碼 4.1.0：2017 年 6 月發行或更新版本|
|Azure CLI v1     | 版本號碼 0.10.13：2017 年 5 月發行或更新版本|
|AzCopy           | 版本號碼 6.1.0：2017 年 6 月發行或更新版本|

Azure CLI v2 和 Azure 儲存體總管的 hello 支援即將推出。 

**針對非受控磁碟或分頁 Blob，是否支援 P4 和 P6 磁碟大小？**

否。 只有受控磁碟才支援 P4 (32 GB) 和 P6 (64 GB) 磁碟大小。 即將支援非受控磁碟和分頁 Blob。

**如果我管理的現有 premium 磁碟小於 hello 少數磁碟啟用 （大約是 2017 年 6 月 15) 之前，已建立 64 GB，如何為它收費？**

現有的小型高階磁碟不超過 64 GB 繼續計費 toobe 相應 toohello P10 定價層。 

**我可以切換 hello 磁碟層小於 64 GB 的小型高階磁碟從 P10 tooP4 或 P6？**

您可以擷取您的小型磁碟的快照，然後建立 定價層 tooP4 磁碟 tooautomatically 交換器 hello 或 P6 根據 hello 佈建大小。 


## <a name="what-if-my-question-isnt-answered-here"></a>如果這裡沒有解答我的問題該怎麼辦？

如果這裡未列出您的問題，請告訴我們，我們將協助您找到答案。 您可以將在 hello 本文結尾處將問題張貼 hello 註解中。 tooengage 與 hello Azure 儲存體小組及其他社群成員關於本文中，使用 hello MSDN [Azure 儲存體論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)。

toorequest 功能提交您的要求和意見 toohello [Azure 儲存體意見反應論壇](https://feedback.azure.com/forums/217298-storage)。
