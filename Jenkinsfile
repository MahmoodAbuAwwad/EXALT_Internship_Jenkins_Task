pipeline{
  agent any
  stages{
    stage("checkout"){
      steps{
        echo "====== Checkout Github Repo. ======"
        checkout([
            $class: 'GitSCM',
            branches: scm.branches,
            extensions: scm.extensions + [[$class: 'master'], [$class: 'WipeWorkspace']],
            userRemoteConfigs: [[url: 'https://github.com/MahmoodAbuAwwad/Internship_Jenkins_Task.git']],
            doGenerateSubmoduleConfigurations: false
        ])
      }
    }
    stage("Build"){
      steps{
        echo "===== Building ====="
      }
    }
  }
}
