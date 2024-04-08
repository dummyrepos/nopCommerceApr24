pipeline {
    agent {
        label 'nop'
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('scm') {
            steps {
                git url: 'https://github.com/dummyrepos/nopCommerceApr24.git',
                    branch: 'develop'
            }
        }
        stage('build') {
            steps {
                //sh 'dotnet publish -o published/ -c Release src/Presentation/Nop.Web/Nop.Web.csproj'
                dotnetPublish configuration: 'Release',
                    outputDirectory: 'published',
                    project: 'src/Presentation/Nop.Web/Nop.Web.csproj'

            }
            post {
                success {
                    zip zipFile: 'nop.web.zip',
                      archive: true,
                      dir: './published',
                      overwrite: true
                }
            }
        }

    }
}