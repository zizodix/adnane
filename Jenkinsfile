pipeline {
    agent any

    environment {
        BUILD_OUTPUT_DIR = "build_output/"
        UNIT_TEST_OUTPUT = "test_output/unit_tests/"
        FUNCTIONAL_TEST_OUTPUT = "test_output/functional_tests/"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Compiling the code...'
                sh 'mkdir -p ${BUILD_OUTPUT_DIR}'
                sh 'echo "This is a simulated build artifact." > ${BUILD_OUTPUT_DIR}artifact.txt'
                echo 'Build completed.'
            }
            post {
                success {
                    archiveArtifacts artifacts: '${BUILD_OUTPUT_DIR}**', onlyIfSuccessful: true
                }
            }
        }

        stage('Unit Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mkdir -p ${UNIT_TEST_OUTPUT}'
                sh 'echo "Simulating unit test execution and results."'
                sh 'echo "<testsuite tests=\'1\'><testcase classname=\'foo\' name=\'bar\' time=\'0.001\'></testcase></testsuite>" > ${UNIT_TEST_OUTPUT}unit_tests_report.xml'
                echo 'Unit tests passed.'
            }
            post {
                always {
                    junit '${UNIT_TEST_OUTPUT}unit_tests_report.xml'
                }
            }
        }

        stage('Functional Test') {
            steps {
                echo 'Running functional tests...'
                sh 'mkdir -p ${FUNCTIONAL_TEST_OUTPUT}'
                sh 'echo "Simulating functional test execution and results."'
                sh 'echo "<testsuite tests=\'2\'><testcase classname=\'foo\' name=\'bar1\' time=\'0.002\'></testcase><testcase classname=\'foo\' name=\'bar2\' time=\'0.003\'></testcase></testsuite>" > ${FUNCTIONAL_TEST_OUTPUT}functional_tests_report.xml'
                echo 'Functional tests passed.'
            }
            post {
                always {
                    junit '${FUNCTIONAL_TEST_OUTPUT}functional_tests_report.xml'
                }
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying application...'
                sh 'echo "Deployment logic goes here. This could involve SSH, kubectl, or cloud provider CLI commands."'
                echo 'Application deployed.'
            }
        }
    }
}
