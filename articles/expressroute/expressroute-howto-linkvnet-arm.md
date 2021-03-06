<properties 
   pageTitle="PowerShell を使用した ExpressRoute 回線への仮想ネットワークのリンク | Microsoft Azure"
   description="このドキュメントでは、Resource Manager デプロイメント モデルと PowerShell を使用して ExpressRoute 回線に仮想ネットワーク (VNet) をリンクする方法の概要について説明します。"
   services="expressroute"
   documentationCenter="na"
   authors="ganesr"
   manager="carmonm"
   editor=""
   tags="azure-resource-manager"/>
<tags 
   ms.service="expressroute"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="infrastructure-services"
   ms.date="06/09/2016"
   ms.author="ganesr" />

# ExpressRoute 回線への仮想ネットワークのリンク

> [AZURE.SELECTOR]
- [Azure ポータル - Resource Manager](expressroute-howto-linkvnet-portal-resource-manager.md)
- [PowerShell - Resource Manager](expressroute-howto-linkvnet-arm.md)
- [PowerShell - クラシック](expressroute-howto-linkvnet-classic.md)


この記事では、Resource Manager デプロイメント モデルと PowerShell を使用して Azure ExpressRoute 回線に仮想ネットワーク (VNet) をリンクする方法について説明します。仮想ネットワークは、同じサブスクリプションにあっても、別のサブスクリプションの一部であってもかいまいません。

**Azure のデプロイ モデルについて**

[AZURE.INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## 構成の前提条件

- Azure PowerShell モジュールの最新バージョン (バージョン 1.0 以降) が必要になります。PowerShell コマンドレットのインストールの詳細については、「[Azure PowerShell のインストールおよび構成方法](../powershell-install-configure.md)」を参照してください。
- 構成を開始する前に、[前提条件](expressroute-prerequisites.md)、[ルーティングの要件](expressroute-routing.md)、[ワークフロー](expressroute-workflows.md)を確認する必要があります。
- アクティブな ExpressRoute 回線が必要です。 
	- 手順に従って、[ExpressRoute 回線を作成](expressroute-howto-circuit-arm.md)し、接続プロバイダー経由で回線を有効にしてください。 
	- 回線用に Azure プライベート ピアリングが構成されていることを確認してください。ルーティング手順については、[ルーティングの構成](expressroute-howto-routing-arm.md)に関する記事を参照してください。 
	- Azure プライベート ピアリングが構成されていることを確認します。また、エンド ツー エンド接続を有効にできるように、ネットワークと Microsoft の間の BGP ピアリングを起動しておく必要があります。
	- 仮想ネットワークと仮想ネットワーク ゲートウェイを作成し、完全にプロビジョニングします。[VPN ゲートウェイ](../articles/vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)を作成する手順に従いますが、必ず `-GatewayType ExpressRoute` を使用してください。

最大 10 個の仮想ネットワークを ExpressRoute 回線に接続できます。ExpressRoute 回線はすべて同じ地理的リージョンにある必要があります。ExpressRoute Premium アドオンを有効にした場合は、ExpressRoute 回線に多数の仮想ネットワークをリンクできます。Premium アドオンの詳細については、[FAQ](expressroute-faqs.md) を確認してください。

## 同じサブスクリプション内の仮想ネットワークを回線に接続する

次のコマンドレットを使用し、ExpressRoute 回線に仮想ネットワーク ゲートウェイを接続できます。コマンドレットを実行する前に、仮想ネットワーク ゲートウェイが作成されており、リンクの準備ができていることを確認してください。

	$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
	$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
	$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute

## 別のサブスクリプション内の仮想ネットワークを回線に接続する

複数のサブスクリプションで ExpressRoute 回線を共有できます。下図に、複数のサブスクリプションで ExpressRoute 回線を共有するしくみについて概略を示します。

大規模クラウド内のそれぞれの小規模クラウドは、組織内のさまざまな部門に属するサブスクリプションを表すために使用されています。組織内の各部門はサービスのデプロイ用に固有のサブスクリプションを使用できますが、1 つの ExpressRoute 回線を共有することで、オンプレミス ネットワークに接続し直すことができます。1 つの部門 (この例では IT) で ExpressRoute 回線を所有できます。組織内の他のサブスクリプションも ExpressRoute 回線を使用できます。

>[AZURE.NOTE] 専用回線の接続と帯域幅の料金は、ExpressRoute 回線の所有者が負担することになります。すべての仮想ネットワークが同じ帯域幅を共有します。

![サブスクリプション間接続](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### 管理

*回線所有者*は、ExpressRoute 回線リソースの権限のあるパワー ユーザーです。回線所有者は、*回線ユーザー*が利用できる承認を作成できます。*回線ユーザー*は、(ExpressRoute 回線とは別のサブスクリプション内にある) 仮想ネットワーク ゲートウェイの所有者です。*回線ユーザー*は、承認を利用できます (仮想ネットワークごとに 1 つの承認)。

*回線所有者*は、承認をいつでも変更し、取り消す権限を持っています。承認を取り消すと、アクセスが取り消されたサブスクリプションからすべてのリンク接続が削除されます。

### 回線所有者の操作 

#### 承認の作成
	
回線所有者は、承認を作成します。その結果、回線ユーザーが各自の仮想ネットワーク ゲートウェイを ExpressRoute 回線に接続するために使用できる承認キーが作成されます。承認は、1 つの接続に対してのみ有効です。

次のコマンドレット スニペットは、承認を作成する方法を示しています。

	$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
	Add-AzureRmExpressRouteCircuitAuthorization -Circuit $circuit -Name "MyAuthorization1"
	Set-AzureRmExpressRouteCircuit -Circuit $circuit

	$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -Circuit $circuit -Name "MyAuthorization1"
		

このコマンドレットの応答に、承認キーと状態が含まれます。

	Name                   : MyAuthorization1
	Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
	Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
	AuthorizationKey       : ####################################
	AuthorizationUseStatus : Available
	ProvisioningState      : Succeeded

		

#### 承認の確認

回線所有者は、次のコマンドレットを実行し、特定の回線で発行されるすべての承認を確認できます。

	$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
	$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -Circuit $circuit
	

#### 承認の追加

回線所有者は、次のコマンドレットを使用して承認を追加できます。

	$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
	Add-AzureRmExpressRouteCircuitAuthorization -Circuit $circuit -Name "MyAuthorization2"
	Set-AzureRmExpressRouteCircuit -Circuit $circuit
	
	$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
	$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -Circuit $circuit

	
#### 承認の削除

回線所有者は、次のコマンドレットを実行して、ユーザーに対する承認を取り消したり削除したりすることができます。

	Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
	Set-AzureRmExpressRouteCircuit -Circuit $circuit	

### 回線ユーザーの操作

回線ユーザーは、ピア ID と回線所有者が作成した承認キーを必要とします。承認キーは GUID です。

#### 接続承認の利用

回線ユーザーは次のコマンドレットを実行し、リンク承認を利用できます。

	$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"	
	$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"

#### 接続承認の解除

ExpressRoute 回線を仮想ネットワークにリンクしている接続を削除することで、承認を解除できます。

## 次のステップ

ExpressRoute の詳細については、「[ExpressRoute のFAQ](expressroute-faqs.md)」をご覧ください。

<!---HONumber=AcomDC_0615_2016-->