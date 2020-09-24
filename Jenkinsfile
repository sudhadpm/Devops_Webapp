node {

    stage('Code Checkout'){

      git credentialsId: 'githubcreds', url: 'https://github.com/sudhadpm/Devops_Webapp.git'  

    }

    

    stage('Build, Test and Package'){

        

       

        def mavenHome = tool name: 'maven-3' , type:'maven'

        def mavenCMD = "{mavenHome}/bin/mvn"

      sh "${mavenCMD} clean package"

       sh "${mavenCMD} test"

    }

    

    stage('Build Docker Image'){

        sh 'sudo docker build -t sudhadpm/devopsjenkins:1.0.0.0 .'

    }

    

    stage("Docker"){

        withCredentials([string(credentialsId: 'dockerHubcred', variable: 'dockerHubCreds')]) {

        sh 'sudo docker login -u sudhadpm -p ${dockerHubcred}'

}

sh 'sudo docker push sudhadpm/devopsjenkins:1.0.0.0'

    }

    

    stage('Run the Docker Image'){

        sh 'sudo docker run -p 8886:8080 -d sudhadpm/devopsjenkins:1.0.0.0'

    }

    

}