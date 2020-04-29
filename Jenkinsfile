node {
   checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'GITHUB', url: 'https://github.com/Saiteju1997/jfrog.git']]]) // Obtain an Artifactory server instance, defined in Jenkins --> Manage:
    def server = Artifactory.server 'jfrog'

    // Read the upload spec which was downloaded from github.
    def uploadSpec = readFile 'ArtifactoryPipeline.zip'
    // Upload to Artifactory.
    def buildInfo1 = server.upload spec: uploadSpec
   
    // Read the download spec and download files from Artifactory.
    def downloadSpec = readFile 'exclude-download.json'
    def buildInfo2 = server.download spec: downloadSpec

    // Merge the upload and download build-info objects.
     buildInfo1.append buildInfo2

    // Publish the build to Artifactory
     server.publishBuildInfo buildInfo1
}
