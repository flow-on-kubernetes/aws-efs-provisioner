## Provision efs(Shared Storage Service) on aws

After running script successfully terminal will display commands to deploy helm chart

Script to provision efs on aws. 

### Prerequisite:
    Python 2 version 2.7+ or Python 3 version 3.4+

### steps:
    1) Install aws cli
        a) pip3 install awscli

    2) Configure aws cli
        a) aws configure
            AWS Access Key ID: <AWS Access Key ID>
            AWS Secret Access Key: <AWS Secret Access Key>
            Default region name: <region>
            Default output format: <text|table|json>

    3) Run script
        ./efs-provision.sh --action <create|delete> --efs-name <name> --vpc-id <vpc-xxxxx> --region <region>

        where:
            action              =   create | delete
            efs-name            =   efs name
            vpc-id              =   vpc id 
            region              =   region
            performance-mode    =   generalPurpose | maxIO (Optional)
            throughput-mode     =   provisioned | bursting (Optional)
            throughput          =   in mbps, Only if --throughput is provisioned

    4) Deploy helm chart
    
        helm repo add stable https://kubernetes-charts.storage.googleapis.com/
        helm repo update
        helm install <name> stable/efs-provisioner --set efsProvisioner.efsFileSystemId=<file system id> --set efsProvisioner.awsRegion=<region> --set efsProvisioner.dnsName=<filesystem ip
