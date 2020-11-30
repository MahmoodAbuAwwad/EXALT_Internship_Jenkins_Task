pipeline{
  agent any
  stages{
    stage("checkout"){
      steps{
        echo "====== Checkout Github Repo. ======"
        git 'https://github.com/MahmoodAbuAwwad/Internship_Jenkins_Task.git'
        sh "git checkout master"
      }
    }
    stage("Build"){
      steps{
        echo "===== Building ====="
      }
    }
  }
}
