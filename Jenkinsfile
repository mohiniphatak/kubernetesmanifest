node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email phatakmohini@gmail.com"
                        sh "git config user.name mohiniphatak"
                        
                        // sh "cat deployment.yaml"
                        //sh "sed -i 's+monikartik11/gitops-terraform-jenkins.*+monikartik11/gitops-terraform-jenkins:${DOCKERTAG}+g' deployment.yaml"
                        sh "sed -i 's+monikartik11/gitops-terraform-jenkins.*+monikartik11/gitops-terraform-jenkins:${DOCKERTAG}+g' deployment.yaml"

                        sh "cat deployment.yaml"
                        sh "git add deployment.yaml"
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git pull https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git"
                        
                        
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
