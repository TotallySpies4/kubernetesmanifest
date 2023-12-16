node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'git', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email raj@cloudwithraj.com"
                        sh "git config user.name RajSaha"
                        //sh "git switch master"
                        sh "cat lstm-deployment.yaml"
                        sh "cat frontend-deployment.yaml"
                        sh "cat backend-deployment.yaml"
                        sh "sed -i 's+siri0000/lstm_model_image.*+siri0000/lstm_model_image:${DOCKERTAG}+g' lstm-deployment.yaml"
                        sh "sed -i 's+siri0000/frontend_image.*+siri0000/frontend_image:${DOCKERTAG}+g' frontend-deployment.yaml"
                        sh "sed -i 's+siri0000/backend_image.*+siri0000/backend_image:${DOCKERTAG}+g' backend-deployment.yaml"
                        sh "cat lstm-deployment.yaml"
                        sh "cat frontend-deployment.yaml"
                        sh "cat backend-deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/TotallySpies4/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
