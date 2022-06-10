pipeline {
    agent any

    stages {
        stage('Source'){
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/feature/**']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/engboustani/TestMinimalApi.git']]])
            }
        }
        stage('Build') {
            steps {
                powershell 'mkdir "$env:systemdrive\inetpub\testsite"'
                powershell 'dotnet build -o "$env:systemdrive\inetpub\testsite"'
                powershell 'New-IISSite -Name "TestSite" -BindingInformation "*:8888:" -PhysicalPath "$env:systemdrive\inetpub\testsite"'
            }
        }
    }
}