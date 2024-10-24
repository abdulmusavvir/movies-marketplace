def imageName = 'abdulmusavvirrohe/movies-marketplace'
node(){
    stage('code checkout'){
        checkout scm
    }
    def imageTest = docker.build("${imageName}-test","-f Dockerfile.test .")
    stage('Pre-Integration Tests'){
        parallel(
            'Quality Test':{
                sh 'docker build -t ${imageName}-test -f Dockerfile.test .'
                sh 'docker run -rm ${imageBame}-test run lint'
            },
            'Code Coverage':{
                sh "docker run --rm -v $PWD/coverage:/app/coverage ${imageName}-test npm run test"            
                publishHTML (target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: "$PWD/coverage/marketplace",
                    reportFiles: "index.html",
                    reportName: "Coverage Report"
                    ])
            }
                )
    }
}
