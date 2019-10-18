---
title: Rete virtuale tra più sedi simulata in Azure
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 07/09/2018
audience: ITPro
ms.topic: article
ms.service: o365-solutions
localization_priority: Priority
search.appverid:
- MET150
ms.collection:
- Ent_O365
- Strat_O365_Enterprise
ms.custom:
- Ent_TLGs
ms.assetid: 0a3555dc-6f96-49a5-b9e2-7760e16630b3
description: 'Riepilogo: creare una rete virtuale cross-premise simulata in Microsoft Azure come ambiente di sviluppo/test.'
ms.openlocfilehash: 595aa20595f43f481aaf090a14d0d7c0df000345
ms.sourcegitcommit: 36e760407a1f4b18bc108134628ed9a8d3e35a8a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/17/2019
ms.locfileid: "34162489"
---
# <a name="simulated-cross-premises-virtual-network-in-azure"></a><span data-ttu-id="37a38-103">Rete virtuale tra più sedi simulata in Azure</span><span class="sxs-lookup"><span data-stu-id="37a38-103">Simulated cross-premises virtual network in Azure</span></span>

 <span data-ttu-id="37a38-104">**Riepilogo:** creare una rete virtuale cross-premise simulata in Microsoft Azure come ambiente di sviluppo/test.</span><span class="sxs-lookup"><span data-stu-id="37a38-104">**Summary:** Create a simulated cross-premises virtual network in Microsoft Azure as a dev/test environment.</span></span>
  
<span data-ttu-id="37a38-p101">In questo articolo viene mostrato come creare un ambiente basato su cloud con Microsoft Azure usando due reti virtuali Azure. Di seguito è riportata la configurazione risultante.  </span><span class="sxs-lookup"><span data-stu-id="37a38-p101">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks. Here is the resulting configuration.</span></span> 
  
![Fase 3 dell'ambiente di sviluppo/test della rete virtuale cross-premise simulata, con la macchina virtuale DC2 nella rete virtuale XPrem](media/df458c56-022b-4688-ab18-056c3fd776b4.png)
  
<span data-ttu-id="37a38-108">Questa simula un ambiente di produzione cloud ibrido in IaaS di Azure ed è costituita da:</span><span class="sxs-lookup"><span data-stu-id="37a38-108">This simulates an Azure IaaS hybrid cloud production environment and consists of:</span></span>
  
- <span data-ttu-id="37a38-109">Una rete locale simulata e semplificata, ospitata in una rete virtuale di Azure (la rete virtuale TestLab).</span><span class="sxs-lookup"><span data-stu-id="37a38-109">A simulated and simplified on-premises network hosted in an Azure virtual network (the TestLab virtual network).</span></span>
    
- <span data-ttu-id="37a38-110">Una rete virtuale cross-premise simulata ospitata in Azure (XPrem).</span><span class="sxs-lookup"><span data-stu-id="37a38-110">A simulated cross-premises virtual network hosted in Azure (XPrem).</span></span>
    
- <span data-ttu-id="37a38-111">Una relazione peering di rete virtuale tra le due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="37a38-111">A VNet peering relationship between the two virtual networks.</span></span>
    
- <span data-ttu-id="37a38-112">Un controller di dominio secondario nella rete virtuale XPrem.</span><span class="sxs-lookup"><span data-stu-id="37a38-112">A secondary domain controller in the XPrem virtual network.</span></span>
    
<span data-ttu-id="37a38-113">Tale configurazione fornisce una base e un punto di partenza comune da cui è possibile:</span><span class="sxs-lookup"><span data-stu-id="37a38-113">This provides a basis and common starting point from which you can:</span></span> 
  
- <span data-ttu-id="37a38-114">Sviluppare e testare applicazioni in un ambiente cloud ibrido simulato in IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="37a38-114">Develop and test applications in a simulated Azure IaaS hybrid cloud environment.</span></span>
    
- <span data-ttu-id="37a38-115">Creare configurazioni di test dei computer, alcune all'interno della rete virtuale TestLab e alcune all'interno della rete virtuale XPrem, per simulare carichi di lavoro IT basati su cloud ibridi.</span><span class="sxs-lookup"><span data-stu-id="37a38-115">Create test configurations of computers, some within the TestLab virtual network and some within the XPrem virtual network, to simulate hybrid cloud-based IT workloads.</span></span>
    
<span data-ttu-id="37a38-116">Le fasi principali della configurazione dell'ambiente di sviluppo e testing sono tre:</span><span class="sxs-lookup"><span data-stu-id="37a38-116">There are three major phases to setting up this dev/test environment:</span></span>
  
1. <span data-ttu-id="37a38-117">Configurare la rete virtuale TestLab.</span><span class="sxs-lookup"><span data-stu-id="37a38-117">Configure the TestLab virtual network.</span></span>
    
2. <span data-ttu-id="37a38-118">Creare la rete virtuale cross-premise.</span><span class="sxs-lookup"><span data-stu-id="37a38-118">Create the cross-premises virtual network.</span></span>
    
3. <span data-ttu-id="37a38-119">Configurare DC2.</span><span class="sxs-lookup"><span data-stu-id="37a38-119">Configure DC2.</span></span>
    
> [!NOTE]
> <span data-ttu-id="37a38-120">Questa configurazione richiede una sottoscrizione a pagamento di Azure.</span><span class="sxs-lookup"><span data-stu-id="37a38-120">This configuration requires a paid Azure subscription.</span></span> 
  
![Guide dei laboratori di testing nel cloud Microsoft](media/24ad0d1b-3274-40fb-972a-b8188b7268d1.png)
  
> [!TIP]
> <span data-ttu-id="37a38-122">Fare clic [qui](http://aka.ms/catlgstack) per consultare una mappa di tutti gli articoli nella serie di guide dei lab di test di Office 365.</span><span class="sxs-lookup"><span data-stu-id="37a38-122">Click [here](http://aka.ms/catlgstack) for a visual map to all the articles in the Office 365 Test Lab Guide stack.</span></span>
  
## <a name="phase-1-configure-the-testlab-virtual-network"></a><span data-ttu-id="37a38-123">Fase 1: configurare la rete virtuale TestLab</span><span class="sxs-lookup"><span data-stu-id="37a38-123">Phase 1: Configure the TestLab virtual network</span></span>

<span data-ttu-id="37a38-124">Utilizzare le istruzioni disponibili in [Configurazione base ambiente di sviluppo/test](base-configuration-dev-test-environment.md) per configurare i computer DC1, APP1 e CLIENT1 nella rete virtuale di Azure denominata TestLab.</span><span class="sxs-lookup"><span data-stu-id="37a38-124">Use the instructions in [Base Configuration dev/test environment](base-configuration-dev-test-environment.md) to configure the DC1, APP1, and CLIENT1 computers in the Azure virtual network named TestLab.</span></span>
  
<span data-ttu-id="37a38-125">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="37a38-125">This is your current configuration.</span></span> 
  
![Fase 4 della configurazione base in Azure con la macchina virtuale CLIENT1](media/25a010a6-c870-4690-b8f3-84421f8bc5c7.png)
  
## <a name="phase-2-create-the-xprem-virtual-network"></a><span data-ttu-id="37a38-127">Fase 2: creare la rete virtuale XPrem</span><span class="sxs-lookup"><span data-stu-id="37a38-127">Phase 2: Create the XPrem virtual network</span></span>

<span data-ttu-id="37a38-128">In questa fase, viene creata e configurata la nuova rete virtuale XPrem, viene quindi eseguita la connessione alla rete virtuale TestLab con peering di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="37a38-128">In this phase, you create and configure the new XPrem virtual network and then connect it to the TestLab virtual network with VNet peering.</span></span>
  
<span data-ttu-id="37a38-129">Innanzitutto, avviare un prompt dei comandi di Azure PowerShell sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="37a38-129">First, start an Azure PowerShell prompt on your local computer.</span></span>
  
> [!NOTE]
> <span data-ttu-id="37a38-p102">I seguenti comandi consentono di utilizzare la versione più recente di Azure PowerShell. Vedere [Panoramica dei cmdlet di Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="37a38-p102">The following command sets use the latest version of Azure PowerShell. See [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/).</span></span> 
  
<span data-ttu-id="37a38-132">Accedere al proprio account di Azure con questo comando.</span><span class="sxs-lookup"><span data-stu-id="37a38-132">Sign in to your Azure account with this command.</span></span>
  
```
Connect-AzAccount
```

<!--
> [!TIP]
> Click [here](https://gallery.technet.microsoft.com/PowerShell-commands-for-7844edd0) to get a text file that has all of the PowerShell commands in this article.
-->
  
<span data-ttu-id="37a38-133">Ottenere il nome della sottoscrizione con questo comando.</span><span class="sxs-lookup"><span data-stu-id="37a38-133">Get your subscription name using this command.</span></span>
  
```
Get-AzSubscription | Sort Name | Select Name
```

<span data-ttu-id="37a38-p103">Impostare la sottoscrizione di Azure. Sostituire tutto il testo racchiuso tra virgolette, compresi i caratteri \< e >, con il nome corretto.</span><span class="sxs-lookup"><span data-stu-id="37a38-p103">Set your Azure subscription. Replace everything within the quotes, including the \< and > characters, with the correct names.</span></span>
  
```
$subscrName="<subscription name>"
Select-AzSubscription -SubscriptionName $subscrName
```

<span data-ttu-id="37a38-136">Successivamente, creare la rete virtuale XPrem e proteggerla con un gruppo di sicurezza di rete con questi comandi.</span><span class="sxs-lookup"><span data-stu-id="37a38-136">Next, create the XPrem virtual network and protect it with a network security group with these commands.</span></span>
  
```
$rgName="<name of the resource group that you used for your TestLab virtual network>"
$locName=(Get-AzResourceGroup -Name $rgName).Location
$Testnet=New-AzVirtualNetworkSubnetConfig -Name "Testnet" -AddressPrefix 192.168.0.0/24
New-AzVirtualNetwork -Name "XPrem" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $Testnet -DNSServer 10.0.0.4
$rule1=New-AzNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP to all VMs on the subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
New-AzNetworkSecurityGroup -Name "Testnet" -ResourceGroupName $rgName -Location $locName -SecurityRules $rule1
$vnet=Get-AzVirtualNetwork -ResourceGroupName $rgName -Name XPrem
$nsg=Get-AzNetworkSecurityGroup -Name "Testnet" -ResourceGroupName $rgName
Set-AzVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "Testnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg
$vnet | Set-AzVirtualNetwork
```

<span data-ttu-id="37a38-137">Creare quindi la relazione peering di rete virtuale tra le reti virtuali TestLab e XPrem con questi comandi.</span><span class="sxs-lookup"><span data-stu-id="37a38-137">Next, you create the VNet peering relationship between the TestLab and XPrem VNets with these commands.</span></span>
  
```
$rgName="<name of the resource group that you used for your TestLab virtual network>"
$vnet1=Get-AzVirtualNetwork -ResourceGroupName $rgName -Name TestLab
$vnet2=Get-AzVirtualNetwork -ResourceGroupName $rgName -Name XPrem
Add-AzVirtualNetworkPeering -Name TestLab2XPrem -VirtualNetwork $vnet1 -RemoteVirtualNetworkId $vnet2.Id
Add-AzVirtualNetworkPeering -Name XPrem2TestLab -VirtualNetwork $vnet2 -RemoteVirtualNetworkId $vnet1.Id
```

<span data-ttu-id="37a38-138">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="37a38-138">This is your current configuration.</span></span> 
  
![Fase 2 dell'ambiente di sviluppo/test della rete virtuale cross-premise simulata, con la relazione di peering della rete virtuale e la rete virtuale XPrem](media/cac5e999-69c7-4f4c-bfce-a7f4006115ef.png)
  
## <a name="phase-3-configure-dc2"></a><span data-ttu-id="37a38-140">Fase 3: configurare DC2</span><span class="sxs-lookup"><span data-stu-id="37a38-140">Phase 3: Configure DC2</span></span>

<span data-ttu-id="37a38-141">In questa fase, viene creata la macchina virtuale DC2 nella rete virtuale XPrem e viene configurata come controller di dominio di replica.</span><span class="sxs-lookup"><span data-stu-id="37a38-141">In this phase, you create the DC2 virtual machine in the XPrem virtual network and then configure it as a replica domain controller.</span></span>
  
<span data-ttu-id="37a38-p104">Innanzitutto, creare una macchina virtuale per DC2. Eseguire questi comandi al prompt dei comandi di Azure PowerShell nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="37a38-p104">First, create a virtual machine for DC2. Run these commands at the Azure PowerShell command prompt on your local computer.</span></span>
  
```
$rgName="<your resource group name>"
$locName=(Get-AzResourceGroup -Name $rgName).Location
$vnet=Get-AzVirtualNetwork -Name XPrem -ResourceGroupName $rgName
$pip=New-AzPublicIpAddress -Name DC2-PIP -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
$nic=New-AzNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
$vm=New-AzVMConfig -VMName DC2 -VMSize Standard_A1
$cred=Get-Credential -Message "Type the name and password of the local administrator account for DC2."
$vm=Set-AzVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
$vm=Set-AzVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version "latest"
$vm=Add-AzVMNetworkInterface -VM $vm -Id $nic.Id
$vm=Set-AzVMOSDisk -VM $vm -Name "DC2-OS" -DiskSizeInGB 128 -CreateOption FromImage -StorageAccountType "Standard_LRS"
$diskConfig=New-AzDiskConfig -AccountType "Standard_LRS" -Location $locName -CreateOption Empty -DiskSizeGB 20
$dataDisk1=New-AzDisk -DiskName "DC2-DataDisk1" -Disk $diskConfig -ResourceGroupName $rgName
$vm=Add-AzVMDataDisk -VM $vm -Name "DC2-DataDisk1" -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
New-AzVM -ResourceGroupName $rgName -Location $locName -VM $vm
```

<span data-ttu-id="37a38-144">Successivamente, eseguire la connessione alla nuova macchina virtuale DC2 dal [portale Azure](https://portal.azure.com) tramite nome dell’account e password dell’amministratore locale. </span><span class="sxs-lookup"><span data-stu-id="37a38-144">Next, connect to the new DC2 virtual machine from the [Azure portal](https://portal.azure.com) using its local administrator account name and password.</span></span>
  
<span data-ttu-id="37a38-p105">Configurare quindi una regola di Windows Firewall per consentire la verifica di connettività di base del traffico. Eseguire questi comandi in DC2 al prompt dei comandi di Windows PowerShell a livello di amministratore. </span><span class="sxs-lookup"><span data-stu-id="37a38-p105">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing. From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span> 
  
```
Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
ping dc1.corp.contoso.com
```

<span data-ttu-id="37a38-p106">Il comando ping dovrebbe produrre quattro risposte dall'indirizzo IP 10.0.0.4. Si tratta di un test del traffico attraverso la relazione peering di rete virtuale. </span><span class="sxs-lookup"><span data-stu-id="37a38-p106">The ping command should result in four successful replies from IP address 10.0.0.4. This is a test of traffic across the VNet peering relationship.</span></span> 
  
<span data-ttu-id="37a38-149">Successivamente, aggiungere un ulteriore disco dati come nuovo volume con lettera di unità F: con questo comando in DC2 al prompt dei comandi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37a38-149">Next, add the extra data disk as a new volume with the drive letter F: with this command from the Windows PowerShell command prompt on DC2.</span></span>
  
```
Get-Disk | Where PartitionStyle -eq "RAW" | Initialize-Disk -PartitionStyle MBR -PassThru | New-Partition -AssignDriveLetter -UseMaximumSize | Format-Volume -FileSystem NTFS -NewFileSystemLabel "WSAD Data"
```

<span data-ttu-id="37a38-p107">Configurare quindi DC2 come controller di dominio di replica per il dominio corp.contoso.com. Eseguire questi comandi dal prompt dei comandi di Windows PowerShell su DC2.</span><span class="sxs-lookup"><span data-stu-id="37a38-p107">Next, configure DC2 as a replica domain controller for the corp.contoso.com domain. Run these commands from the Windows PowerShell command prompt on DC2.</span></span>
  
```
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"
```

<span data-ttu-id="37a38-152">Tenere presente che viene richiesto di fornire sia la password CORP\\User1 che una password per la modalità ripristino servizi directory, nonché di riavviare DC2. </span><span class="sxs-lookup"><span data-stu-id="37a38-152">Note that you are prompted to supply both the CORP\\User1 password and a Directory Services Restore Mode (DSRM) password, and to restart DC2.</span></span> 
  
<span data-ttu-id="37a38-p108">Ora che la rete virtuale XPrem dispone di un proprio server DNS (DC2), è necessario configurare la rete virtuale XPrem per utilizzarlo. Eseguire questi comandi nel computer locale al prompt dei comandi di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37a38-p108">Now that the XPrem virtual network has its own DNS server (DC2), you must configure the XPrem virtual network to use this DNS server. Run these commands from the Azure PowerShell command prompt on your local computer.</span></span>
  
```
$vnet=Get-AzVirtualNetwork -ResourceGroupName $rgName -name "XPrem"
$vnet.DhcpOptions.DnsServers="192.168.0.4" 
Set-AzVirtualNetwork -VirtualNetwork $vnet
Restart-AzVM -ResourceGroupName $rgName -Name "DC2"
```

<span data-ttu-id="37a38-p109">Utilizzare le credenziali CORP\\User1 per eseguire la connessione a DC1 dal portale di Azure sul computer locale. Per configurare il dominio CORP in modo che computer e utenti utilizzino il controller di dominio locale per l'autenticazione, eseguire questi comandi in DC1 al prompt dei comandi di Windows PowerShell a livello di amministratore.</span><span class="sxs-lookup"><span data-stu-id="37a38-p109">From the Azure portal on your local computer, connect to DC1 with the CORP\\User1 credentials. To configure the CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>
  
```
New-ADReplicationSite -Name "TestLab" 
New-ADReplicationSite -Name "XPrem"
New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "XPrem"
```

<span data-ttu-id="37a38-157">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="37a38-157">This is your current configuration.</span></span> 
  
![Fase 3 dell'ambiente di sviluppo/test della rete virtuale cross-premise simulata, con la macchina virtuale DC2 nella rete virtuale XPrem](media/df458c56-022b-4688-ab18-056c3fd776b4.png)
  
<span data-ttu-id="37a38-159">L’ambiente cloud ibrido di Azure simulato è ora pronto per eseguire test.</span><span class="sxs-lookup"><span data-stu-id="37a38-159">Your simulated Azure hybrid cloud environment is now ready for testing.</span></span>
  
## <a name="next-step"></a><span data-ttu-id="37a38-160">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="37a38-160">Next step</span></span>

<span data-ttu-id="37a38-161">Utilizzare l’ambiente di sviluppo/test per simulare un [Server di SharePoint Intranet 2016 nell'ambiente di sviluppo/test in Azure](https://technet.microsoft.com/library/mt806351%28v=office.16%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="37a38-161">Use this dev/test environment to simulate a [SharePoint Server 2016 intranet farm hosted in Azure](https://technet.microsoft.com/library/mt806351%28v=office.16%29.aspx).</span></span>
  
## <a name="see-also"></a><span data-ttu-id="37a38-162">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="37a38-162">See Also</span></span>

[<span data-ttu-id="37a38-163">Ambiente di sviluppo/test della configurazione di base</span><span class="sxs-lookup"><span data-stu-id="37a38-163">Base Configuration dev/test environment</span></span>](base-configuration-dev-test-environment.md)
  
[<span data-ttu-id="37a38-164">Ambiente di sviluppo/test di Office 365</span><span class="sxs-lookup"><span data-stu-id="37a38-164">Office 365 dev/test environment</span></span>](office-365-dev-test-environment.md)
  
[<span data-ttu-id="37a38-165">DirSync per l'ambiente di sviluppo/test di Office 365</span><span class="sxs-lookup"><span data-stu-id="37a38-165">DirSync for your Office 365 dev/test environment</span></span>](dirsync-for-your-office-365-dev-test-environment.md)
  
[<span data-ttu-id="37a38-166">Protezione avanzata dalle minacce per l'ambiente di sviluppo/test di Office 365</span><span class="sxs-lookup"><span data-stu-id="37a38-166">Advanced Threat Protection for your Office 365 dev/test environment</span></span>](advanced-threat-protection-for-your-office-365-dev-test-environment.md)
  
[<span data-ttu-id="37a38-167">Adozione del cloud e soluzioni ibride</span><span class="sxs-lookup"><span data-stu-id="37a38-167">Cloud adoption and hybrid solutions</span></span>](cloud-adoption-and-hybrid-solutions.md)


