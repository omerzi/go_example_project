// Run the job every 5 minutes 
CRON_SETTINGS = '''*/5 * * * *'''

pipeline {
    agent any

    triggers {
        cron(CRON_SETTINGS)
    }

    environment {
        // [Mandatory only for projects which use npm, yarn 2, NuGet and .NET to download their dependencies]
        // The command that installs the project dependencies (e.g "npm i", "nuget restore" or "dotnet restore")
        JF_INSTALL_DEPS_CMD= "npm i"

        // [Mandatory]
        // JFrog platform URL (This functionality requires version 3.29.0 or above of Xray)
        JF_URL= "https://ecosysjfrog.jfrog.io/"

        // [Mandatory if JF_ACCESS_TOKEN is not provided]
        // JFrog user and password with 'read' permissions for Xray
        // JF_USER= credentials("JF_USER")
        // JF_PASSWORD= credentials("JF_PASSWORD")

        // [Mandatory]
        // Bitbucket accesses token with the following permissions 
        JF_GIT_TOKEN= credentials("JF_GIT_TOKEN")
        JF_GIT_PROVIDER= "github"

        // [Mandatory]
        // Bitbucket project namespace
        JF_GIT_OWNER= "omerzi"

        // [Mandatory]
        // Bitbucket repository name
        // JF_GIT_REPO= 'yahavi'
        JF_GIT_BASE_BRANCH= 'master'
        // JF_GIT_PULL_REQUEST_ID=0

        // [Mandatory]
        // API endpoint to Bitbucket server
        // JF_GIT_API_ENDPOINT= "https://git.jfrog.info/rest"

        // Uncomment the below options if you'd like to use them.

        // [Mandatory if JF_USER and JF_PASSWORD are not provided]
        // JFrog access token with 'read' permissions for Xray
        // JF_ACCESS_TOKEN= credentials("JF_ACCESS_TOKEN")

        // [Optional, default: "."]
        // Relative path to the project in the git repository
        // JF_WORKING_DIR= path/to/project/dir

        // [Optional]
        // Xray Watches. Learn more about them here: https://www.jfrog.com/confluence/display/JFROG/Configuring+Xray+Watches
        // JF_WATCHES= <watch-1>,<watch-2>...<watch-n>

        // [Optional]
        // JFrog project. Learn more about it here: https://www.jfrog.com/confluence/display/JFROG/Projects
        // JF_PROJECT= <project-key>

        // [Optional, default: "FALSE"]
        // Displays all existing vulnerabilities, including the ones that were added by the pull request.
        // JF_INCLUDE_ALL_VULNERABILITIES= "TRUE"

        // [Optional, default: "TRUE"]
        // Fails the Frogbot task if any security issue is found.
        // JF_FAIL= "FALSE"
    }

   stages {
    //   stage('Download Frogbot') {
    //      steps {
    //         // For Linux / MacOS runner:
    //         // sh """ curl -fLg "https://releases.jfrog.io/artifactory/frogbot/v2/[RELEASE]/getFrogbot.sh" | sh"""
            

    //         // For Windows runner:
    //         // powershell """iwr https://releases.jfrog.io/artifactory/frogbot/v2/[RELEASE]/frogbot-windows-amd64/frogbot.exe -OutFile .\frogbot.exe"""
    //         }
    //     }

        stage ('Scan Pull Requests') {
            steps {
                sh "chmod +x frogbot"
                sh "./frogbot scan-pull-requests"

                // For Windows runner:
                // powershell """.\frogbot.exe scan-pull-requests"""
            }
        }
    }
}