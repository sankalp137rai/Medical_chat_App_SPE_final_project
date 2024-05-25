pipeline {
    agent any

    environment {
        // Retrieve the sudo password from Jenkins credentials and set it as an environment variable
        SUDO_PASSWORD = credentials('SUDO_PASSWORD')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sankalp137rai/SPE_final_project.git'
            }
        }

        // stage('Build Docker Frontend Image') {
        //     steps {
        //         dir('healthcare_chatbot_frontend') {
        //             script {
        //                 frontendImage = docker.build("sankalp137rai/react-app:frontend")
        //             }
        //         }
        //     }
        // }

        // stage('Push Docker Frontend Image') {
        //     steps {
        //         script {
        //             withDockerRegistry([credentialsId: "DockerHubCred", url: ""]) {
        //                 frontendImage.push()
        //             }
        //         }
        //     }
        // }

        // stage('Build Docker Backend Image') {
        //     steps {
        //         dir('healthcare_chatbot_backend') {
        //             script {
        //                 backendImage = docker.build("sankalp137rai/flask-app:backend")
        //             }
        //         }
        //     }
        // }

        // stage('Push Docker Backend Image') {
        //     steps {
        //         script {
        //             withDockerRegistry([credentialsId: "DockerHubCred", url: ""]) {
        //                 backendImage.push()
        //             }
        //         }
        //     }
        // }
        // stage('Deploy with Ansible') {
        //     steps {
        //         script {
        //             ansiblePlaybook becomeUser: null, colorized: true, disableHostKeyChecking: true, installation: 'Ansible', inventory: 'ansible-deploy/inventory',
        //             playbook: './ansible-deploy/ansible-book.yml', sudoUser: null
        //         }
        //     }
        // }

        // stages {
        //         stage('Deploy to Minikube using ansible') {
        //             steps {
        //                 script {
        //                     // Export the sudo password and run the Ansible playbook
        //                     sh '''
        //                         export SUDO_PASSWORD=${SUDO_PASSWORD}
        //                         ansible-playbook /home/sankalp/Documents/healthcareChatbot/ansible-deploy/ansible-book.yml -i /home/sankalp/Documents/healthcareChatbot/ansible-deploy/inventory
        //                     '''
        //                 }
        //             }
        //         }
        //     }
        // }
        // stages {
        //     stage('Deploy with Ansible') {
        //         steps {
        //             script {
        //                 // Export the sudo password and run the Ansible playbook using the ansiblePlaybook step
        //                 withEnv(["SUDO_PASSWORD=${SUDO_PASSWORD}"]) {
        //                     ansiblePlaybook becomeUser: null, 
        //                                     colorized: true, 
        //                                     disableHostKeyChecking: true, 
        //                                     installation: 'Ansible', 
        //                                     inventory: './ansible-deploy/inventory', 
        //                                     playbook: './ansible-deploy/ansible-book.yml', 
        //                                     sudoUser: null,
        //                                     extraVars: [ansible_sudo_pass: SUDO_PASSWORD]
        //                 }
        //             }
        //         }
        //     }
        // }
        stage('Deploy with Ansible') {
            steps {
                script {
                    withEnv(["SUDO_PASSWORD=${SUDO_PASSWORD}"]) {
                        ansiblePlaybook becomeUser: null, 
                                        colorized: true, 
                                        disableHostKeyChecking: true, 
                                        installation: 'Ansible', 
                                        inventory: 'ansible-deploy/inventory', 
                                        playbook: './ansible-deploy/ansible-book.yml', 
                                        sudoUser: null,
                                        extraVars: [ansible_become_pass: SUDO_PASSWORD]
                    }
                }
            }
        }

        // stage('Deploy frontend to Kubernetes') {
        //     steps {
        //         dir('kubernates') {
        //             script {
        //                 sh "kubectl apply -f frontend.yaml"
        //             }
        //         }
        //     }
        // }
    }
}
