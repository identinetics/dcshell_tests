// pipeline tools require python3 env with jinja2, pytest and pyyaml installed for jenkins shell scripts

pipeline {
    agent any
    options { disableConcurrentBuilds() }

    stages {
        stage('Test1') {
            steps {
                sh '''
                    export DOCKER_REGISTRY_USER=jenkins
                    ./dcshell//update_config.sh dc_test1.yaml.default dc_test1.yaml
                    export BASH_TRACE=1
                    source ./jenkins_scripts.sh
                    remove_containers alpinista && echo '.'
                    export MANIFEST_SCOPE='local'
                    export PROJ_HOME='.'
                    ./dcshell/build -D $PWD -f dc_test1.yaml
                '''
            }
        }
    }
    post {
        always {
            sh '''
                source ./jenkins_scripts.sh
                remove_containers alpinista && echo '.'
            '''
        }
    }
}
