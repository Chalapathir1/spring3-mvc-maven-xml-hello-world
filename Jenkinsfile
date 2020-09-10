pipeline {
    agent any
	tools{
	maven "maven3"
	}
    stages {
        stage('Git SCM') {
            steps {
                git credentialsId: 'github_credentials', url: 'https://github.com/Chalapathir1/spring3-mvc-maven-xml-hello-world.git'
                
            }
        }
	stage('initilize') {
            steps {
                sh '''echo "PATH = ${PATH}"
                      echo "M2_HOME = ${M2_HOME}"
		   '''
            }
        }
	stage('Build'){
		steps{
		sh 'mvn -f pom.xml clean package'
		}
	}
	stage('Deploye'){
		steps{
		deploy adapters: [tomcat8(credentialsId: 'tomcat_credentials', path: '', url: 'http://ec2-13-234-35-27.ap-south-1.compute.amazonaws.com:8080/')], contextPath: 'Hello_Pipeline', onFailure: false, war: '**/target/*.war'
		}
	}

    }
}
