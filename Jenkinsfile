pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven 3.8.1"
    }

    stages {
        stage('Get source code') {
            steps {
                git branch : 'dev', credentialsId : 'mounika', url : 'https://github.com/mounikadevidivi/maven-web-application.git'
            }
        }
        // stage('deployToNexus') {
        //     steps {
        //         withCredentials([usernamePassword(credentialsId: 'nexus-creds', usernameVariable: 'NEXUS_USER', passwordVariable: 'NEXUS_PASS')]) {
        //             writeFile file: 'custom-settings.xml', text: """
        //             <settings>
        //               <servers>
        //                 <server>
        //                   <id>mvn-pipeline-proj</id>
        //                   <username>${NEXUS_USER}</username>
        //                   <password>${NEXUS_PASS}</password>
        //                 </server>
        //               </servers>
        //             </settings>
        //             """
        //             sh 'mvn -s custom-settings.xml -Dmaven.test.failure.ignore=true clean deploy'
        //         }
        //     }
        // }
        
        // stage('DeplotToTomcat') {
        //     steps {
        //         deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat-admin', path: '', url: 'http://172.31.210.7:9090/')], contextPath: 'maven-app', war: '**/*.war'
        //     }
        // }
        
        stage('Sonar Analysis') {
            steps {
                //echo 'Sonar Analysis.....'
                //here sonar: sonarqube servername
                withSonarQubeEnv('mySonarqube') {
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
    }
}
