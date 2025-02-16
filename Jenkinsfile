pipeline{
    agent any
    stages {
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/shaikharbaaz101/Hotstar-Clone.git'
            }
        }
        stage('Terraform version'){
             steps{
                 sh 'terraform --version'
             }
        }
        stage('Terraform init'){
             steps{
                 dir('EC2_TERRAFORM') {
                      sh 'terraform init'
                   }
             }
        }
        // stage('Terraform validate'){
        //      steps{
        //          dir('EC2_TERRAFORM') {
        //               sh 'terraform validate'
        //            }
        //      }
        // }
        stage('Terraform plan'){
             steps{
                 dir('EC2_TERRAFORM') {
                      sh 'terraform plan'
                   }
             }
        }
        // stage('Terraform apply/destroy'){
        //      steps{
        //          dir('EC2_TERRAFORM') {
        //               sh 'terraform ${action} --auto-approve'
        //            }
        //      }
        // }
    }
}
