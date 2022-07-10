
*) Move vm to another resouce group

Get-AzResource -ResourceGroupName WB01_GROUP | Format-table -wrap -Property ResourceId

Get-AzVM  -status -name wb01

Stop-AzVM -ResourceGroupName "web-dev" -Name "wb01" -Confirm

Start-AzVM -ResourceGroupName "web-dev" -Name "wb01" 

Get-AzVM -ResourceGroupName "web-dev" -Name "wb01" 

Get-AzPublicIpAddress -Name myPublicIp*


$PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
$PasswordProfile.Password = "Azuew2022#"
New-AzureADUser -DisplayName "Sibi Sundaram" -PasswordProfile $PasswordProfile -UserPrincipalName "sibi@contoso.com" -AccountEnabled $true -MailNickName "sibi"

*) list modules

Get-Module -ListAvailable Az.Network 


*) Lock on storage account
$resourceGroupName = "web-dev"
$storageAccountName = "sunnystorageaccount10"

New-AzResourceLock -LockName LockStorage -LockLevel CanNotDelete -ResourceGroupName $resourceGroupName -ResourceName $storageAccountName -ResourceType Microsoft.Storage/storageAccounts


Get-AzResourceLock -ResourceGroupName $resourceGroupName -ResourceName $storageAccountName -ResourceType Microsoft.Storage/storageAccounts

$lockId = (Get-AzResourceLock -ResourceGroupName $resourceGroupName -ResourceName $storageAccountName -ResourceType Microsoft.Storage/storageAccounts).LockId
Remove-AzResourceLock -LockId $lockId

Remove-AzStorageAccount -ResourceGroupName $resourceGroupName -AccountName $storageAccountName

*) Add disk

$rgName = 'web-dev'
$vmName = 'wb01'
$location = 'Australia East'
$storageType = 'Premium_LRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzDiskConfig -SkuName $storageType -Location $location -CreateOption Empty -DiskSizeGB 5
$dataDisk1 = New-AzDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzVM -Name $vmName -ResourceGroupName $rgName
$vm = Add-AzVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzVM -VM $vm -ResourceGroupName $rgName



$vm = Get-AzVM -Name $vmName -ResourceGroupName $rgName
Remove-AzVMDataDisk  -VM $vm    -Name "wb01_datadisk1"
Update-AzVM  -ResourceGroupName $rgName -vm $vm

Remove-AzDisk -ResourceGroupName $rgName -DiskName $dataDiskName