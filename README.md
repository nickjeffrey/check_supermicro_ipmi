# check_supermicro_ipmi
 nagios check to query IPMI service processor on SuperMicro motherboard to read temperature sensors, fan speeds, etc.


## Requirements
perl, snmpwalk, snmpget on nagios server
IP address configured on IPMI service processor with SNMP enabled


## Configuration
You will need a section in the services.cfg
file on the nagios server that looks similar to the following.
```
      # Define a service to check the SuperMicro IPMI
      # Parameters are SNMP community name
      define service {
              use                             generic-service
              hostgroup_name                  all_supermicro_ipmi
              service_description             SuperMicro IPMI
              check_command                   check_supermicro_ipmi!public
              }
```

You will also need a command definition similar to the following in commands.cfg on the nagios server
```
      # 'check_supermicro_ipmi' command definition
      # parameters are -H hostname -C snmp_community
      define command{
              command_name    check_supermicro_ipmi
              command_line    $USER1$/check_supermicro_ipmi -H $HOSTADDRESS$ -C $ARG1$
              }
```



## Output
Output will look similar to the following:
```
SuperMicro IPMI OK - System temperature:37C  CPU temperature:53C  DIMM-A1 temperature:37C DIMM-B1 temperature:37C PCH temperature:49C Fan1:5200rpm FanB:5300rpm | system_temperature=37;45;40;; cpu_temperature=53;65;60;;
```
