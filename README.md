![ee](https://github.com/user-attachments/assets/7b946d15-a65c-4520-ba28-00edd997c63f)



# Jenkins Pipeline Project

This project demonstrates a Jenkins pipeline setup with dynamic stage execution based on user input. The pipeline is designed to handle multiple scripting languages and execute specific stages depending on the selected language. The source code, including the `Jenkinsfile`, is hosted on GitHub.

## Project Overview

The objective of this project was to create a Jenkins pipeline that:
1. **Triggers Automatically**: Initiates a build process after each commit to the repository.
2. **Choice Parameter**: Uses a choice parameter to determine which language-specific stages to execute.
3. **Dynamic Stage Execution**: Executes only the relevant stages based on the selected language.

## Key Features

- **Choice Parameter**: The pipeline includes a choice parameter named `Language` with the following values:
  - `All` (default)
  - `C`
  - `Python`
  - `Bash`

- **Conditional Stage Execution**: Depending on the value selected for the `Language` parameter, the pipeline executes only the stages related to that language, while skipping others.

- **Pipeline Stages**: The pipeline includes a minimum of 3-4 stages, each dedicated to running scripts in different languages.

## Pipeline Configuration

### Jenkinsfile

The core of this project is the `Jenkinsfile`, which defines the pipeline and its stages. The `Jenkinsfile` includes:
- **Trigger Configuration**: Automatically triggers a build for every commit.
- **Choice Parameter**: A dropdown for selecting the programming language.
- **Conditional Logic**: Executes stages based on the selected language.

Here is a simplified version of the `Jenkinsfile`:

```groovy
pipeline {
    agent any
    
    parameters {
        choice(name: 'Language', choices: ['All', 'C', 'Python', 'Bash'], description: 'Select the language to execute.')
    }
    
    stages {
        stage('Build C') {
            when {
                expression { params.Language == 'All' || params.Language == 'C' }
            }
            steps {
                sh './build_c_script.sh'
            }
        }
        
        stage('Build Python') {
            when {
                expression { params.Language == 'All' || params.Language == 'Python' }
            }
            steps {
                sh './build_python_script.sh'
            }
        }
        
        stage('Build Bash') {
            when {
                expression { params.Language == 'All' || params.Language == 'Bash' }
            }
            steps {
                sh './build_bash_script.sh'
            }
        }
        
        stage('Notify') {
            steps {
                echo 'Pipeline execution complete.'
            }
        }
    }
}
```

### Repository Structure

The repository contains the following files:

- **`Jenkinsfile`**: Defines the pipeline stages and logic.
- **`build_c_script.sh`**: Script for C language build.
- **`build_python_script.sh`**: Script for Python language build.
- **`build_bash_script.sh`**: Script for Bash language build.

## Setup and Usage

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/EladDafna/Jenkins_Project.git
   ```
   
2. **Configure Jenkins**:
   - Create a new pipeline job in Jenkins.
   - Point the job to the GitHub repository URL.
   - Ensure the pipeline is configured to trigger on every commit.

3. **Run the Pipeline**:
   - Choose a language from the `Language` parameter dropdown.
   - Start the build to execute the relevant stages.

## Conclusion

This project showcases how to use Jenkins pipelines with dynamic stage execution based on user input. It helps in automating the build process for multiple programming languages and streamlines the continuous integration workflow.

Feel free to explore the repository and adapt the pipeline configuration to fit your specific needs!
