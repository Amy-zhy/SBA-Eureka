pipeline {
  agent any
  environment {
    DOCKERHUBNAME = "zhanghongyu423"
  }
  stages {
    stage('Build') {
      steps {
        echo 'build starting...'
        // bat 'mvn clean'
        // echo 'maven clean successfully...'
        // bat 'mvn install -DskipTests=true -Dmaven.javadoc.skip=true -B -V'
        // bat 'mvn -B -DskipTests clean package'
        // echo 'maven install successfully...'
        // bat 'mvn package'
        echo 'maven clean and package successfully!'
      }
    }
    stage('Build Docker Image') {
      steps {
        echo "Starting building..."
        // bat 'cd C:\\Users\\HongYuZhang\\.jenkins\\workspace\\erueka_master\\target'
        // bat 'dir'
        // bat 'copy "C:\\Users\\HongYuZhang\\.jenkins\\workspace\\erueka_master\\target\\eureka-server-1.0-SNAPSHOT.jar" "C:\\Jenkinstest"'
        // bat 'copy "C:\\Users\\HongYuZhang\\.jenkins\\workspace\\erueka_master\\target\\eureka-server-1.0-SNAPSHOT.jar" "C:\\jenkinsdocker"'
        // echo 'copy jar successfully!'
        // bat 'java -jar C:\\Jenkinstest\\eureka-server-1.0-SNAPSHOT.jar'
        // echo 'start jar successfully!!!'

        // bat 'docker build -f C:\\Users\\HongYuZhang\\Desktop\\fullstack-eurekaserver\\Dockerfile -t eureka C:\\Users\\HongYuZhang\\Desktop\\fullstack-eurekaserver\\target'
        // bat 'docker images'
        // bat 'docker run -d -p 9999:8761 eureka'  
        // bat 'docker ps' 
        withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          echo '%USERNAME%'
          echo '%PASSWORD%'
          // bat 'docker login -u $USERNAME -p $PASSWORD'
          bat 'docker login -u %USERNAME% -p %PASSWORD%'
          echo 'Start building image...'
          bat 'docker image build -t %DOCKERHUBNAME%/sbaamyeureka .'
          echo 'Image build successfully!'
          echo 'Start pushing image to docker hub...'
          bat 'docker push %DOCKERHUBNAME%/sbaamyeureka'
          echo 'Image push successfully!'
          echo 'Start running...'
          bat 'docker run -d -p 8761:8761 --name sba-eureka %DOCKERHUBNAME%/sbaamyeureka'
          echo 'docker running successfully!'
        }   
      }
    }
  }
  post {
    always {
      echo 'build and deploy finished'
    }

    failure {
      echo 'build failed'
    }

    success {
      echo 'deploy successfully'
    }
  }
}