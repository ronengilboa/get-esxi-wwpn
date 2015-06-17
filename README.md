# get-esxi-wwpn
#get esxi hba wwpn, in 3 ways
#get-view is the fastest, so when doing mass - use that 

### get-vmhosthba
$esxi = get-vmhost -name esxi1.xxx.com
$esxi | Get-VMHostHba | select @{N="WWN";E={"{0:X}" -f $_.PortWorldWideName}}

###get-view
$v = Get-View -ViewType hostsystem -Filter @{name='esxi1.xxx.com'}
$v.Config.StorageDevice.HostBusAdapter | select @{N="WWN";E={"{0:X}" -f $_.PortWorldWideName}}


###using extension data
$esxi.ExtensionData.Config.StorageDevice.HostBusAdapter | select @{N="WWN";E={"{0:X}" -f $_.PortWorldWideName}}
