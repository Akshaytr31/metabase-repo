pipeline{
  agent any
  stages{
    stage("Git Checkout”){
      steps{
       git branch: 'main', credentialsId: '6f9b1e58-14d2-4d2a-8bfd-613e76ccf480', url: 'https://github.com/Akshaytr31/metabase-repo.git'
      }
    }
  }
}
