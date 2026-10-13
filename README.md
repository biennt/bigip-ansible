# Demo of using Ansible to automate F5 BIG-IP Configuration
## Setup the environment
```
python3 -m venv venv
source venv/bin/activate
pip install f5-sdk
pip install bigsuds
pip install ansible
```
Edit the inventory file.
```
[lb]
bigip ansible_host=10.0.1.152 ansible_user=devops

[webservers]
10.0.1.[5:10]
```

Create the Ansible Vault password file: vars_encrypted.yml (clear text, storing the big-ip password)

```
bigip_pass: MatKhauRatBiMat123!
```
Encrypt the file:
```
ansible-vault encrypt vars_encrypted.yml
```

Run the playbook, to test the settings (before doing anything else)
```
ubuntu@ip-10-0-1-23:~$ ansible-playbook -i ansible_inventory --ask-vault-pass bigip-facts.yml
Vault password:

PLAY [GRAB F5 FACTS] ******************************************************************************************************************************

TASK [COLLECT BIG-IP FACTS] ***********************************************************************************************************************
[WARNING]: Host 'bigip' is using the discovered Python interpreter at '/home/ubuntu/venv/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered. See https://docs.ansible.com/ansible-core/2.21/reference_appendices/interpreter_discovery.html for more information.
ok: [bigip]

TASK [DISPLAY COMPLETE BIG-IP SYSTEM INFORMATION] *************************************************************************************************
ok: [bigip] => {
    "device_facts": {
        "ansible_facts": {
            "ansible_net_queried": true,
            "ansible_net_system_info": {
                "base_mac_address": "02:ff:e5:4a:37:ad",
                "chassis_serial": "624b27ec-7782-d3b3-7855c4c4fbe9",
                "hardware_information": [
                    {
                        "model": "AMD EPYC 7R32",
                        "name": "cpus",
                        "type": "base-board",
                        "versions": [
                            {
                                "name": "cache size",
                                "version": "512 KB"
                            },
                            {
                                "name": "cores",
                                "version": "8  (physical:4)"
                            },
                            {
                                "name": "cpu MHz",
                                "version": "2799.992"
                            },
                            {
                                "name": "cpu sockets",
                                "version": "1"
                            },
                            {
                                "name": "cpu stepping",
                                "version": "0"
                            }
                        ]
                    }
                ],
                "marketing_name": "BIG-IP Virtual Edition",
                "package_edition": "Point Release 2",
                "package_version": "Build 0.0.22 - Mon Aug 24 05:36:56 PDT 2026",
                "platform": "Z100",
                "product_build": "0.0.22",
                "product_build_date": "Mon Aug 24 05:36:56 PDT 2026",
                "product_built": 260824053656,
                "product_changelist": 3955606,
                "product_code": "BIG-IP",
                "product_jobid": 1573062,
                "product_version": "21.1.0.2",
                "time": {
                    "day": 13,
                    "hour": 13,
                    "minute": 39,
                    "month": 10,
                    "second": 11,
                    "year": 2026
                },
                "uptime": 4872
            },
            "discovered_interpreter_python": "/home/ubuntu/venv/bin/python3.12"
        },
        "changed": false,
        "deprecations": [
            {
                "collection_name": "ansible.builtin",
                "deprecator": {
                    "resolved_name": "ansible.builtin",
                    "type": null
                },
                "msg": "Importing 'to_text' from 'ansible.module_utils._text' is deprecated.",
                "version": "2.24"
            }
        ],
        "failed": false,
        "queried": true,
        "system_info": {
            "base_mac_address": "02:ff:e5:4a:37:ad",
            "chassis_serial": "624b27ec-7782-d3b3-7855c4c4fbe9",
            "hardware_information": [
                {
                    "model": "AMD EPYC 7R32",
                    "name": "cpus",
                    "type": "base-board",
                    "versions": [
                        {
                            "name": "cache size",
                            "version": "512 KB"
                        },
                        {
                            "name": "cores",
                            "version": "8  (physical:4)"
                        },
                        {
                            "name": "cpu MHz",
                            "version": "2799.992"
                        },
                        {
                            "name": "cpu sockets",
                            "version": "1"
                        },
                        {
                            "name": "cpu stepping",
                            "version": "0"
                        }
                    ]
                }
            ],
            "marketing_name": "BIG-IP Virtual Edition",
            "package_edition": "Point Release 2",
            "package_version": "Build 0.0.22 - Mon Aug 24 05:36:56 PDT 2026",
            "platform": "Z100",
            "product_build": "0.0.22",
            "product_build_date": "Mon Aug 24 05:36:56 PDT 2026",
            "product_built": 260824053656,
            "product_changelist": 3955606,
            "product_code": "BIG-IP",
            "product_jobid": 1573062,
            "product_version": "21.1.0.2",
            "time": {
                "day": 13,
                "hour": 13,
                "minute": 39,
                "month": 10,
                "second": 11,
                "year": 2026
            },
            "uptime": 4872
        },
        "warnings": [
            "Host 'bigip' is using the discovered Python interpreter at '/home/ubuntu/venv/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered."
        ]
    }
}

PLAY RECAP ****************************************************************************************************************************************
bigip                      : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
