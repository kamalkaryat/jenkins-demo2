def remote = [:]
remote.name = 'test'
remote.host = '3.83.242.186'
remote.port = 22
remote.allowAnyHosts = true
pipeline {
    agent any
     stages {
        stage('Git Clone') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', credentialsId: 'githubcreds', url: 'https://github.com/kamalkaryat/jenkins-demo2'
            }
        }
     stage('Deployment'){
        steps {
            script {
             // move the new changed 
             sh 'ls'
             withCredentials([usernamePassword(credentialsId: 'ubuntucred', passwordVariable: 'pass', usernameVariable: 'user')]) {
             remote.user = user
             remote.password = pass
             sshPut remote: remote, from: "index.html", into: "/var/www/html"
             sshCommand remote: remote, command: "ls /var/www/html"
             }
           }
          }
        }
      }
    }
