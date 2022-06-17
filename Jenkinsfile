pipeline { 

 

    agent any 



    tools { 



        // Install the Maven version configured as "Maven" and add it to the path. 

 

        maven 'maven' 

    } 

    stages { 



stage("SCM Checkout"){ 



steps{ 



checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/gitz-88/webAppExample.git']]])

} 



} 

        stage('Build') { 

 

            steps { 

 

                // Run Maven on a Unix agent. 



                sh "mvn -Dmaven.test.failure.ignore=true clean package" 



                // To run Maven on a Windows agent, use 



                // bat "mvn -Dmaven.test.failure.ignore=true clean package" 



            } 


            post { 



                // If Maven was able to run the tests, even if some of the test 



                // failed, record the test results and archive the jar file. 

 

                success { 

 

                    archiveArtifacts 'target/*.war' 



                } 



            } 



        } 



        stage('Deploy'){ 

steps { 



deploy adapters: [tomcat9(credentialsId: 'af08b91c-bb46-4d53-b609-3498d108284e', path: '', url: 'http://172.18.254.152:8056/')], contextPath: 'webAppExample', war: '**/*.war'


        } 

} 

    } 

} 
