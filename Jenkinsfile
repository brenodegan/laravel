node('php'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }
    
    stage('Fetch') {
        checkout scm
    }
    
    stage('Build'){
        sh 'composer install --no scripts --prefer-dist --no-dev --ignore-platform-reqs'
    }
    
    stage('config') {
        parallel(
            'config cache': {
                echo 'tarefa paralela 1'
            },
            'config route': {
                echo 'tarefa palela 2'
            }
        )
    }
    stage('Docker Build') {
        sh 'docker build -t brenodegan/laravel:$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push brenodegan/laravel:$BUILD_NUMBER'
    }
}
