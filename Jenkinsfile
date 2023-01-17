

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
    AWS_SECRET_ACCESS_KEY=credentials('AWS_SECRET_ACCESS_KEY')
    AWS_SESSION_TOKEN = credentials('AWS_SESSION_TOKEN')
    }
    
    stages{
        stage('Create network stack'){
            steps{
                sh 'curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"'
                sh 'unzip awscliv2.zip'
                sh ' ./aws/install'
                sh 'aws cloudformation create-stack --stack-name jenkins-network --template-body file://network.yaml \
                --pameters ParameterKey=CIDRBlock,ParameterValue=${CIDRBlock} \
                ParameterKey=PublicSubnetCIDR,ParameterValue=${PublicSubnetCIDR}'
                
            }
        }
    }
}
