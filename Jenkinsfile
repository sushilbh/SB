node('maven'){
    def mvnhome = tool name: 'maven360', type: 'maven'
    
    stage('first stage checking out'){
        echo "checking stage 001"
    }
    
    stage('maven build'){
        sh "$mvnhome/bin/mvn clean test surefire-report:report-only"
    }
    
    stage('publishing test result'){
        junit allowEmptyResults:true, testResults: '/home/ec2-user/workspace/pipeline-for-sanquest/target/surefire-reports/*.xml'
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '', reportFiles: 'index.html', reportName: 'HTMLReport', reportTitles: ''])
    }
    
    stage('packaging software'){
        sh "$mvnhome/bin/mvn clean package"
    }
    
    
    stage('working on to create artifactory'){
        archiveArtifacts '**/target/*.jar'
    }
}
