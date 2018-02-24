node('php56'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }
    
    stage('Fetch') {
        checkout scm
    }
    
    stage('Build App'){
        sh 'composer install --no-scripts --prefer-dist --no-dev --ignore-platform-reqs'
    }
    
    stage('Docker Build') {
        sh 'docker build -t ioricloud/laravel:$BRANCH_NAME-$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push ioricloud/laravel:$BUILD_NUMBER'
        sh 'docker rmi -f ioricloud/laravel:$BUILD_NUMBER'
    }
}
