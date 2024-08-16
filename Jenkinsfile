pipeline {
    agent any
    parameters {
        choice(
            name: 'Language',
            choices: ['All', 'Python', 'C', 'Bash'],
            description: 'Choose the language'
        )
    }
    stages {
        stage('List File - (Step 1)') {
            steps {
                echo "Step 1 is running...."
                script {
                    echo "Workspace: ${WORKSPACE}"
                    sh 'ls -la'
                }
            }
        }
        stage('Choose a File (Step 2)') {
            steps {
                echo "Step 2 is running...."
                script {
                    sh 'pwd'
                    sh 'ls -la'
                    if (params.Language == 'Python' || params.Language == 'Bash' || params.Language == 'C') {
                        sh """
                            echo "Your Choose is:" ${params.Language}
                            cat ${params.Language}.txt
                            mkdir -p ${WORKSPACE}/Language
                            mv ${params.Language}.txt ${WORKSPACE}/Language
                        """
                    } else {
                            echo "The script is automatically started, so your choice is: All "
                            sh """
                                mkdir -p ${WORKSPACE}/Language
                                cp ${WORKSPACE}/*[CBP]*.txt ${WORKSPACE}/Language/
                               """
                    }

                }
            }
        }
        stage('Check the Files - (Step 3)') {
            steps {
                echo "Step 3 is running..."
                script {
                    sh """
                        cd ${WORKSPACE}/Language/
                        ls -la
                        cat *
                        """
                }
            }
        }
    }
}
