def workDir = "/home/remote_user/workspace/Task_JenkinsFile"
pipeline{
  agent any
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
        label 'slave'
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
                    error("Build failed, no Memory Available")
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
  }
}
