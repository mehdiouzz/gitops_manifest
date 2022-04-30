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
                        sh "git config user.email el.mehdi.ouazzane@gmail.com"
                        sh "git config user.name mehdiouzz"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "cp deployment.yaml deployment${DOCKERTAG}.yaml"
                        sh "sed -i 's+mehdiouzz/test.*+mehdiouzz/test:${DOCKERTAG}+g' deployment${DOCKERTAG}.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/gitops_manifest.git HEAD:main"
      }
    }
  }
}
}
