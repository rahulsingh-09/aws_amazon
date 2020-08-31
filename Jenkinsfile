pipeline {
    agent { label 'ansible-poc' }
    stages {
        stage ('Git Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: https://github.com/appu-rajiv/poc-deploy-webapp.git]]])
            }
        }
        stage ('Deploy Webapp') {
            steps {
                script {
                    writeFile(file: 'ansible_inv', text: ANSIBLE_INVENTORY)
                }
                sh("ansible-playbook -i ansible_inv web.yml -v")
            }
        }
        stage ('API Testing') {
            agent { label 'docker-poc'}
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: https://github.com/appu-rajiv/poc-selenium-robot.git]]])
                sh("docker build -t robot .")
                sh("docker run -e SERVER_URL=http://${WEBAPP_IP}:${WEBAPP_PORT} -v " + "\'${WORKSPACE}/testsuites:/workspace\' robot")
            }
        }
    }
}
