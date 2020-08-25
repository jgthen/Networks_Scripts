# Script to perform backups in cisco routers or switches

from netmiko import ConnectHandler
from datetime import date
import os.path



ip_devices = ['192.168.122.4', '192.168.122.5']

time=date.today()
for devices in ip_devices:

    net_devices = {
        'device_type':'cisco_ios',
        'ip': devices,
        'username':'admin',
        'password':'cisco'
    }

    net_connect = ConnectHandler(**net_devices)
    output = net_connect.send_command("show runn")
    save_path = '/var/backups/' # path where the backups will be saved
    namebackup = 'backup-'+devices+str('-')+str(time)
    pathbackup = os.path.join(save_path,namebackup )
    file = open(pathbackup,"w")
    file.write(output)
    file.close()
