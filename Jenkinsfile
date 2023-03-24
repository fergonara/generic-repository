pipeline {
  parameters {
    choice(name: 'STAGE', choices: ['Build', 'Docker', 'Build+Docker', 'Deploy', 'All'], description: 'Stage to activate');
    string(name: 'S3BUCKET', defaultValue: 'service-builtservices', description: 'AWS S3 bucket where to store classess or retrieve them.');
    string(name: 'DESTENVIRONMENT', defaultValue: '', description: 'Destination environment for the deployment');
    string(name: 'VERSION', defaultValue: '', description: 'Version to copy inside the docker image');
  }
  agent { label 'slave' }
  environment {
    // Jenkins Variables
    workspace="${WORKSPACE}"
    activatedStage = "${params.STAGE}"
    GITREPO = "${sh(script:'echo $GIT_URL | awk -F \'[/ .]\' \'{print $3}\'', returnStdout: true).trim()}"
    versionForDocker = "${params.VERSION}"
    // AWS Variables
    account = "1111111"
    region = "us-west-2"
    s3 = "${params.S3BUCKET}"
    ecr_repo = "ecr-ui-development"
    // service Variables
    env = "${params.DESTENVIRONMENT}"
    DESTENVIRONMENT = "${params.DESTENVIRONMENT}"
    svcName = "service-ui"
    // Filename of the compiled service
    UI_FILES_LOCATION = "s3://${s3}"
    // Compiled version comes from the branch taken to pick the code for the build.
    GITVERSION = "${sh(script:'echo ${GIT_BRANCH///}', returnStdout: true).trim()}"
  }
  stages {
    stage("UI Build dv"){
      when {
        allOf {
          expression { params.STAGE == 'Build' || params.STAGE == 'Build+Docker' || params.STAGE == 'All'};
        }
      }
      agent any
      steps {
        echo "hello"
      }
    }
  }
}