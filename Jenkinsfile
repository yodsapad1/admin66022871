pipeline {
    agent any

    triggers {
        githubPush()  // ทำให้ Pipeline รันอัตโนมัติเมื่อ Push โค้ดขึ้น GitHub
    }

    stages {      
        stage("Checkout Code") {
            steps {
                checkout scm  // ดึงโค้ดจาก GitHub มาใช้
            }
        }

        stage("Copy file to Docker server") {
            steps {
                sshagent(['docker-server-credentials']) {  // ใช้ Jenkins Credentials ในการ SSH
                    sh """
                    scp -r /var/lib/jenkins/workspace/66022871html/* root@43.208.25.201:~/66022871html
                    """
                }
            }
        }
        
        stage("Build Docker Image") {
            steps {
                ansiblePlaybook playbook: '/var/lib/jenkins/workspace/66022871html/playbooks/build.yaml'
            }    
        } 
        
        stage("Create Docker Container") {
            steps {
                ansiblePlaybook playbook: '/var/lib/jenkins/workspace/66022871html/playbooks/deploy.yaml'
            }    
        } 
    }
}
