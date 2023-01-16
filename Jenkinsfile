pipeline{
    
    agent any
    
    parameters{
    string(name: 'CIDRBlock', defaultValue: '', description: 'CIDR block for VPC')
    string(name: 'PublicSubnetCIDR', defaultValue: '', description: 'CIDR block for Public Subnet')
    string(name: 'InstanceType', defaultValue: '', description: 'EC2 Instance Type')
    string(name: 'ImageId', defaultValue: '', description: 'EC2 Image Id')
    string(name: 'KeyPair', defaultValue: '', description: 'Key Pair for EC2')
    }
    
    environment{
    AWS_ACCESS_KEY_ID=credentials('AWS_ACCESS_KEY_ID')
    AWS_ACCESS_KEY_TOKEN=credentials('AWS_ACCESS_KEY_TOKEN')
    }
    
    stages{
        stage('Create network stack'){
            steps{
                sh 'aws cloudformation create-stack --stack-name jenkins-network --template-body file://network.yaml \
                --pameters ParameterKey=CIDRBlock,ParameterValue=${CIDRBlock} \
                ParameterKey=PublicSubnetCIDR,ParameterValue=${PublicSubnetCIDR}'
                
            }
        }
    }
}
