## <a name="scenario"></a>案例
本文將逐步說明一個在 VM 中使用多個 NIC 的部署特殊案例。 在此案例中， Azure 中託管了兩層式 IaaS 工作負載。 在虛擬網路 (VNet) 中每一層皆部署在各自的子網路。 hello 前端層是由數個 web 伺服器，在負載平衡器設定為高可用性群組在一起所組成。 hello 後端層是由數個資料庫伺服器組成。 這些資料庫伺服器會部署兩個 Nic 每個，一個用於資料庫存取權，hello 其他管理。 hello 案例也包含網路安全性群組 (Nsg) toocontrol 哪些允許流量 tooeach 子網路和 NIC hello 部署中。 hello 圖顯示此案例的 hello 基本架構。  

![多個 NIC 案例](./media/virtual-network-deploy-multinic-scenario-include/Figure1.png)

