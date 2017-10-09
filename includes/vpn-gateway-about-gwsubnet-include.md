hello 虛擬網路閘道會使用稱為 hello 'GatewaySubnet' 的特定子網路。 hello 閘道子網路包含 hello hello VPN 閘道服務所使用的 IP 位址。 當您建立閘道子網路時，請將它命名為「GatewaySubnet」。  命名子網路 'GatewaySubnet' 會告訴 Azure toocreate hello 閘道服務的位置。 如果您其他項目命名 hello 子網路，您的 VPN 閘道組態將會失敗。

hello GatewaySubnet hello IP 位址配置 toohello 閘道服務。 當您建立 hello GatewaySubnet 時，您可以指定包含 hello hello 子網路的 IP 位址數目。 您指定的 GatewaySubnet hello hello 大小取決於 hello VPN 閘道設定您想 toocreate。 雖然可能 toocreate GatewaySubnet 越小越/29，我們建議您建立較大的子網路，其中包含多個位址，藉由選取 /27 或/28。 使用較大的閘道子網路允許足夠的 IP 位址 tooaccommodate 可能未來設定。
