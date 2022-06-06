def val = ''
if (params.Datacenter == 'PNQ-Datacenter') {
val = 'PNQ-Datacenter-Agent'
} else if (params.Datacenter == 'HR-Datacenter') {
val = 'HR-Datacenter-Agent'
} 

pipeline {
agent {
	label val
}
stages {
    stage('Set parameters') {
        steps {
            script {
                currentBuild.displayName = '#' + currentBuild.number +
                                            '-' + params.Datacenter
                properties([
                    parameters([
                        [
                            $class: 'ChoiceParameter', 
                            choiceType: 'PT_SINGLE_SELECT', 
                            description: '', 
                            filterLength: 1, 
                            filterable: false, 
                            name: 'Environment', 
                            randomName: 'choice-parameter-4317672109824', 
                            script: [$class: 'GroovyScript', 
                                fallbackScript: [
                                    classpath: [], 
                                    sandbox: true, 
                                    script: ''
                                ], 
                                script: [
                                    classpath: [], 
                                    sandbox: true, 
                                    script: 'return [\'Select an Environment\',\'PROD\', \'DEV\']'
                                ]
                            ]
                        ],
                        [
                            $class: 'CascadeChoiceParameter', 
                            choiceType: 'PT_SINGLE_SELECT', 
                            description: '', 
                            filterLength: 1, 
                            filterable: false, 
                            name: 'Datacenter', 
                            randomName: 'choice-parameter-1434774074254', 
                            referencedParameters: 'Environment', 
                            script: [
                                $class: 'GroovyScript', 
                                fallbackScript: [
                                    classpath: [], 
                                    sandbox: true, 
                                    script: ''
                                ], script: [
                                    classpath: [], 
                                    sandbox: true, 
                                    script: '''
                                        def choices
                                        switch(Environment){
                                            case \'PROD\':
                                                choices = [\'Select a Datacenter\', \'PNQ-Datacenter\', \'HR-Datacenter\']
                                                break
                                            case \'DEV\':
                                                choices = [\'Select a Datacenter\', \'PNQ-Datacenter\', \'HR-Datacenter\']
                                                break
                                            default:
                                                choices = [\'N/A\']
                                                break
                                        }
                                        return choices'''
                                ]
                            ]
                        ],
                        [
                            $class: 'CascadeChoiceParameter', 
                            choiceType: 'PT_SINGLE_SELECT', 
                            description: '', 
                            filterLength: 1, 
                            filterable: false, 
                            name: 'Provision_Server', 
                            randomName: 'choice-parameter-143132192342342254', 
                            referencedParameters: 'Datacenter', 
                            script: [
                                $class: 'GroovyScript', 
                                fallbackScript: [
                                    classpath: [], 
                                    sandbox: true, 
                                    script: ''
                                ], script: [
                                    classpath: [], 
                                    sandbox: true, 
                                    script: '''
                                        def choices
                                        if (Datacenter=='PNQ-Datacenter') {
                                        	choices=['PNQ-Datacenter-Agent']
                                        } else if (Datacenter=='HR-Datacenter') {
                                            choices=['HR-Datacenter-Agent']
                                        } else {
                                            choices=['None']
                                        }
                                        return choices'''
                                ]
                            ]
                        ],
                        string(
                            defaultValue: '', 
                            description: 'Enter your vCenter IP or FQDN', 
                            name: 'vCenter_URL', 
                            trim: true
                        ),
                        string(
                            defaultValue: '', 
                            description: '', 
                            name: 'vSphere_ResourcePool', 
                            trim: true
                        ),
                        [
                            $class: 'CascadeChoiceParameter', 
                            choiceType: 'PT_SINGLE_SELECT', 
                            description: '', 
                            filterLength: 1, 
                            filterable: false, 
                            name: 'vSphere_Datacenter', 
                            randomName: 'choice-parameter-1434323202365329', 
                            referencedParameters: 'Environment, Datacenter', 
                            script: [
                                $class: 'GroovyScript', 
                                fallbackScript: [
                                    classpath: [], 
                                    sandbox: true, 
                                    script: ''
                                ], script: [
                                    classpath: [], 
                                    sandbox: true, 
                                    script: '''
                                        def choices
                                        if (Environment=='PROD') {
                                            choices=['PNQ-Datacenter','HR-Datacenter']
                                        } else if (Datacenter=='DEV') {
                                            choices=['PNQ-Datacenter','HR-Datacenter']
                                        } else {
                                            choices=['None']
                                        }
                                        return choices'''
                                ]
                            ]
                        ],
                        string(
                            defaultValue: 'VM Network', 
                            description: 'Enter the Network for kubernetes node deployment', 
                            name: 'Network_Subnet', 
                            trim: true
                        ),
                        string(
                            defaultValue: '255.255.255.0', 
                            description: '', 
                            name: 'Subnet_Netmask', 
                            trim: true
                        ),
                        string(
                            defaultValue: '', 
                            description: '', 
                            name: 'Default_Gateway', 
                            trim: true
                        ),
                        choice(
                            choices: [
                                'CentOS-7.9-temp'
                            ], 
                            description: '', 
                            name: 'Template'
                        ),
                        string(
                            defaultValue: '', 
                            description: '', 
                            name: 'DNS_Server1', 
                            trim: true
                        ),
                        string(
                            defaultValue: '', 
                            description: '', 
                            name: 'DNS_Server2', 
                            trim: true
                        ),
                        string(
                            defaultValue: '', 
                            description: '', 
                            name: 'DNS_Domain', 
                            trim: true
                        ),
                        string(
                            defaultValue: '', 
                            description: '', 
                            name: 'k8s_master_ip', 
                            trim: true
                        ),
                        string(
                            defaultValue: 'k8s-master', 
                            description: '', 
                            name: 'k8s_master_hostname', 
                            trim: true
                        ),
                        string(
                            defaultValue: '', 
                            description: '', 
                            name: 'k8s_worker01_ip', 
                            trim: true
                        ),
                        string(
                            defaultValue: 'k8s-worker01', 
                            description: '', 
                            name: 'k8s_worker01_hostname', 
                            trim: true
                        ),
                        string(
                            defaultValue: '', 
                            description: '', 
                            name: 'k8s_worker02_ip', 
                            trim: true
                        ),
                        string(
                            defaultValue: 'k8s-worker02', 
                            description: '', 
                            name: 'k8s_worker02_hostname', 
                            trim: true
                        ),
                        string(
                            defaultValue: '', 
                            description: '', 
                            name: 'k8s_worker03_ip', 
                            trim: true
                        ),
                        string(
                            defaultValue: 'k8s-worker03', 
                            description: '', 
                            name: 'k8s_worker03_hostname', 
                            trim: true
                        ),
                        [
                            $class: 'CascadeChoiceParameter', 
                            choiceType: 'PT_SINGLE_SELECT', 
                            description: '', 
                            filterLength: 1, 
                            filterable: false, 
                            name: 'Timezone', 
                            randomName: 'choice-parameter-435671232309824',
                            referencedParameters: 'Datacenter', 
                            script: [$class: 'GroovyScript', 
                                fallbackScript: [
                                    classpath: [], 
                                    sandbox: true, 
                                    script: ''
                                ], 
                                script: [
                                    classpath: [], 
                                    sandbox: true, 
                                    script:  '''
                                        def choices
                                        if (Datacenter=='PNQ-Datacenter') {
                                            choices=['Asia/Kolkata']
                                        } else if (Datacenter=='HR-Datacenter') {
                                            choices=['america/denver']
                                        } else {
                                            choices=['None']
                                        }
                                        return choices'''
                                ]
                            ]
                        ]
                    ])
                ])
            }
        }
    }

    stage ('Replace values in inventory file') {
    	steps {
    		withCredentials([
    			[$class: 'UsernamePasswordMultiBinding', credentialsId: getCredentialsId(),
                usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD'],
                [$class: 'UsernamePasswordMultiBinding', credentialsId: 'centos-login',
                usernameVariable: 'linuxos_username', passwordVariable: 'linuxos_userpassword']]) {
    		sh '''
cp -rf CodePull/* . 

# Variable assignment
masterip=${k8s_master_ip}
node01ip=${k8s_worker01_ip}
node02ip=${k8s_worker02_ip}
node03ip=${k8s_worker03_ip}

masterfqdn=${k8s_master_hostname}
node01fqdn=${k8s_worker01_hostname}
node02fqdn=${k8s_worker02_hostname}
node03fqdn=${k8s_worker03_hostname}

mastervm=${k8s_master_hostname}_${k8s_master_ip}
workernode01=${k8s_worker01_hostname}_${k8s_worker01_ip}
workernode02=${k8s_worker02_hostname}_${k8s_worker02_ip}
workernode03=${k8s_worker03_hostname}_${k8s_worker03_ip}

cat >inventory/dynamic_inventory << EOL
[containerlab]
${mastervm}  Mgmt_network_ipv4=${masterip}  vsphere_vm_hostname=${masterfqdn}
${workernode01} Mgmt_network_ipv4=${node01ip} vsphere_vm_hostname=${node01fqdn}
${workernode02} Mgmt_network_ipv4=${node02ip} vsphere_vm_hostname=${node02fqdn}
${workernode03} Mgmt_network_ipv4=${node03ip} vsphere_vm_hostname=${node03fqdn}

[master]
${masterip}

[workers]
${node01ip}
${node02ip}
${node03ip}

# Node Groups
[nodes:children]
master
workers

[nodes:vars]
ansible_connection=ssh
ansible_user=$linuxos_username
ansible_python_interpreter=/usr/bin/python2.7
ansible_password=$linuxos_userpassword
ansible_ssh_common_args='-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null'
EOL

cat >inventory/group_vars/all.yaml << EOL
# vCenter Login Information
vcenter_hostname: '$vCenter_URL'
vcenter_username: '$USERNAME'
vcenter_password: '$PASSWORD'

# Variable entries for Linux virtual machine
vsphere_datacenter: '$vSphere_Datacenter'
resource_pool: '$vSphere_ResourcePool'

# VM Network Components
Mgmt_network: '$Network_Subnet'
Mgmt_network_nmv4: '255.255.255.0'
Mgmt_network_gwv4: '$Default_Gateway'

# Tempalate of CentOS 7.9 Linux Server
lin_temp: '$Template'
wdc_vm_name: '{{ lin_temp }}'

# Timezone and NTP Server
# Use below command on a linux system to get timezone:
## timedatectl list-timezones
timezone: '$Timezone'
ntp_server:
  - '$DNS_Server1'
  - '$DNS_Server2'

# DNS server details
dns_server1: '$DNS_Server1'
dns_server2: '$DNS_Server2'
dns_domain: '$DNS_Domain'

# Kubernetes Specific Parameters
pod_network: '172.16.0.0/16'   
k8s_master_ip: '${masterip}'   
'''
    		}
    	}
    }

    stage('Nodes Deployment') {
    	steps {
    		echo 'Starting the Kubernetes Nodes deployment....'
            sh """
            ansible-playbook -i inventory containerlab.yaml --tags "deploy"
            """
    	}
    }

    stage('Guest OS Customization') {
    	steps {
    		echo 'Starting the guest os customization'
            sh """
            ansible-playbook -i inventory containerlab.yaml --tags "oscustom"
            """
    	}
    }

    stage('Kubernetes Master Setup') {
        steps {
            echo 'Starting the Kubernetes Master Setup'
            sh """
            ansible-playbook -i inventory containerlab.yaml --tags "mastersetup"
            """
        }
    }

    stage('Kubernetes Nodes Setup') {
        steps {
            echo 'Starting the Kubernetes Node Setup'
            sh """
            ansible-playbook -i inventory containerlab.yaml --tags "nodesetup"
            """
        }
    }

    stage('Kubernetes Nodes labeling') {
        steps {
            echo 'Starting the Kubernetes Nodes Labeling'
            sh """
            ansible-playbook -i inventory containerlab.yaml --tags "nodelabel"
            """
        }
    }

}
}

String getCredentialsId() {
if (params.Environment == "PROD") {
    "vCenter-Login"
} else if (params.Environment == "DEV") {
    "vCenter-Login"
} else {
        "N/A"
    }
}


String getGitUrl() {
    if (params.Environment == "PROD") {
    "https://github.com/Udayendu/vmugdemo03.git"
} else if (params.Environment == "DEV") {
    "https://github.com/Udayendu/vmugdemo03.git"
} else {
        "N/A"
    }
}
