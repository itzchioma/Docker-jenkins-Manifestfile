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
                        sh "git config user.email itzchioma@gmail.com"
                        sh "git config user.name itzchioma"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+itzoma10/test.*+itzoma10/test:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push @github.com/${GIT_USERNAME}/Docker-jenkins-Manifestfile.git">https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Docker-jenkins-Manifestfile.git HEAD:main"
      }
    }
  }
}
}