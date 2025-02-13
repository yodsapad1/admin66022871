pipeline {
    agent any
    stages {      
        stage("Copy file to Docker server") {
            steps {
                // แก้ชื่อ pipeline ให้ตรงกับที่สร้างใน Jenkins
                sh "scp -r /var/lib/jenkins/workspace/66022871html/* root@43.208.25.201:~/66022871html"
            }
        }
        
        stage("Build Docker Image") {
            steps {
                // เรียกใช้ playbook สำหรับ build image
                ansiblePlaybook playbook: '/var/lib/jenkins/workspace/66022871html/playbooks/build.yaml'
            }    
        } 
        
        stage("Create Docker Container") {
            steps {
                // เรียกใช้ playbook สำหรับ deploy container
                ansiblePlaybook playbook: '/var/lib/jenkins/workspace/66022871html/playbooks/deploy.yaml'
            }    
        } 
    }
}
