#Script for find port in switch cisco based in mac address

from netmiko import ConnectHandler
import getpass

print ('''
Network switches
------------------
0 - 192.168.122.4
1 - 192.168.122.5
------------------
''')

user = input('Enter your username: ')
password = getpass.getpass()
device = int(input("Ingress the index of the switch : "))
mac = input('''
Type bellow  the mac address in cisco format example : 0000.0000.0000
Enter mac --> ''')

ip_devices = ['192.168.122.4', '192.168.122.5']

net_devices = {
    'device_type': 'cisco_ios',
    'ip': ip_devices[device],
    'username': 'admin',
    'password': 'cisco'
}

net_connect = ConnectHandler(**net_devices)
command = net_connect.send_command('show mac address-table | i '+(mac))
print("\n")
print ('The port is : '+command[30:]) # # Here must print only the part of the port
print("\n")

