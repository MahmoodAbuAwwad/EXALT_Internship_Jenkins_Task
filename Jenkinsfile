def workDir = "/home/remote_user/workspace/Task_JenkinsFile"
pipeline{
    agent any
    parameters {
      //slave and slave2 are 2 containers with CentosImage connected with jenkins container via ssh
      //configured and added via jenkins gui
      choice(name: 'vm', choices: ['slave', 'slave2'], description: 'Pick VM to deploy on')
    }
    stages{
        stage("clean up"){
            steps{
            echo "====== Cleaning Up. ======"
            sh "rm -rf *"
            }
        }
        stage("checkout"){
            steps{
            echo "====== Checkout Github Repo. ======"
            git credentialsId: 'github', url: 'https://github.com/MahmoodAbuAwwad/Internship_Jenkins_Task.git'
            sh "git checkout master"
            }
        }
        stage("CreatingScript"){
            steps{
            echo "===== Creating Build_number.tar.gz ====="
            sh "tar -cvf ${currentBuild.number}.tar.gz build_number.sh"
            }
        }
        stage("Dilever"){
            steps{
            echo "-============"
            stash name: "tarFile",allowEmpty: true, includes: "${currentBuild.number}.tar.gz"
            }
        }
        stage("DeployOnSlaveMachine"){
            agent {
            label "${params.vm}"
            }
            steps{
            echo "===== Deploying on Slave Machine ====="
            sh "rm -f *.tar.gz"
            unstash 'tarFile'
            sh "tar -xvf ${currentBuild.number}.tar.gz"
            sh "chmod +x build_number.sh"
            echo "---- Printing HostName and MemUsgae% ---"
            sh "./build_number.sh"
            script{
                memUsage=sh(script: './build_number.sh |tail -1',returnStdout: true).trim()
                per = Double.valueOf(memUsage)
                if (per > 80) {
                    stage ('FailAndAlert') {
                    sh 'echo Fail and Alert'
                    }
                }
                if ( per < 80) {
                    stage ('SuccessAndPushToNexus') {
                        sh 'echo Push To NExus'
                    }
                }
            }
            }
        }
        stage('run-parallel-dummy-stages') {
            environment{
                AUTHOR="Mahmoud Hussain"
            }
            failFast true
            parallel {
                stage('List All Files in Working Directory') {
                    agent {
                        label "${params.vm}"
                    }
                    steps {
                        sh "ls ${workDir}"
                    }
                    
                }
                stage('Environment Variable Stage') {
                    agent {
                        label "${params.vm}"
                    }
                    steps {
                        sh 'printenv'
                        //use plugin EnvInject to modify Environment Variables
                    }
                }
            }
        }


    }
     post{
        always{
            echo "======== Always ========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
