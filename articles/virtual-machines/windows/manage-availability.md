---
title: Azure で Windows VM の可用性を管理する
description: 複数の仮想マシンを使って Azure の Windows アプリケーションの高い可用性を確保する方法について説明します。
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: gwallace
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 02351953-7b6a-4657-b9e1-de2ea8f6aa05
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.topic: article
ms.date: 11/27/2019
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f9914b84b63f271c7dd7d1b8f7dbc3b69511605
ms.sourcegitcommit: c31dbf646682c0f9d731f8df8cfd43d36a041f85
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2019
ms.locfileid: "74561186"
---
# <a name="manage-the-availability-of-windows-virtual-machines-in-azure"></a>Azure での Windows 仮想マシンの可用性の管理 

複数の仮想マシンを設定および管理して、Azure の Windows アプリケーションの高い可用性を確保する方法について説明します。 [Linux 仮想マシンの可用性を管理する](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)こともできます。

クラシック デプロイ モデルを使用しているときに、可用性セットを作成および使用する方法については、[可用性セットの構成方法](classic/configure-availability-classic.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)に関するページをご覧ください。

[!INCLUDE [virtual-machines-common-manage-availability](../../../includes/virtual-machines-common-manage-availability.md)]

## <a name="next-steps"></a>次の手順
仮想マシンの負荷分散の詳細については、 [仮想マシンの負荷分散](tutorial-load-balancer.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)に関するページをご覧ください。

IaaS の SQL Server で N 層アプリケーションを実行するための参照アーキテクチャを表示する

* [SQL Server を使用した Azure の Windows N 層アプリケーション](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/n-tier-sql-server)
* [高可用性を得るために複数の Azure リージョンで N 層アプリケーションを実行する](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server)
