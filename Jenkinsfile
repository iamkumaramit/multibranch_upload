
def appName ="Jenkins_test_app"
def namePath = "vars/nestedBranch/CollectionUpload/Deployable/var/collection/var/component/var/${currentBuild.number}"
// def namePath ='' 
def deplyName = 'Test'
def componentUploadResponse =''
def deployableUploadResponse =''
def dataFormat ='json'
def configFile ='config/application/Collection/Collection1/*.json'
def target ='collection'
def commit =true
def validate =true
def convertPath =true
def changesetNumber =''
def finalresponse =''
def chngsetToRegister =''
def regChngeSet =''
def res=''
def collectionName1="Coll_1"
def collectionName2="Coll_2"
pipeline {
    agent any
    stages {
        stage('getData'){
            steps {
                echo 'Checking out files'
                git branch: 'master', url: 'https://github.com/iamkumaramit/samplejava.git'
            }
        }
    
        stage('upload') {
            steps {
                echo "<<<<<<<<<Upload file is starting >>>>>>>>"
                echo "UPLOAD FOR APP: ${appName}"
                echo "TARGET: ${target}"
                echo "CONFIGFILE: ${configFile}"
                echo "NAMEPATH: ${namePath}"
                echo "FORMAT: ${dataFormat}"
                echo "CONVERTPATH: ${convertPath}"
                echo "COMMIT: ${commit}"
                echo "BRANCH NAME: ${env.NODE_NAME}"
          script{
              
               //with changesetNumber and deployable
                componentUploadResponse = snDevOpsConfigUpload(
                    applicationName: "${appName}",
                    deployableName: "${deplyName}",
                    dataFormat: "${dataFormat}",
                    configFile: "${configFile}",
                    target:"${target}",
                    namePath: "${namePath}",
                    //autoCommit:"",
                    autoValidate:"${validate}",
                    changesetNumber:"${changesetNumber}",
                    convertPath:"${convertPath}",
                    collectionName:"${collectionName1}",
                    showResults:true
                    )
                    
                    componentUploadResponse = snDevOpsConfigUpload(
                                        applicationName: "${appName}",
                                        deployableName: "${deplyName}",
                                        dataFormat: "${dataFormat}",
                                        configFile: "${configFile}",
                                        target:"${target}",
                                        namePath: "${namePath}",
                                        autoCommit:"${commit}",
                                        autoValidate:"${validate}",
                                        changesetNumber:"${componentUploadResponse}",
                                        convertPath:"${convertPath}",
                                        collectionName:"${collectionName2}",
                                        showResults:true
                                        )
                
            }
                echo " RESPONSE FROM UPLOAD : ${componentUploadResponse}"
                
            }
        }
        stage('export'){
            steps{
                echo "export started."
                echo " ++++++++++++"
                // snDevOpsChange()
                script{
                // res = snDevOpsConfigRegisterChangeSet(changesetNumber:"${componentUploadResponse}")
                echo "Response from second register: ${res}"
                // snDevOpsConfigGetSnapshots(
                //         applicationName: "${appName}",
                //         changesetNumber: "${componentUploadResponse}",
                //         deployableName: "",
                //         outputFormat:"xml"
                //         )
                }
                
                echo "export finished successfully."
            }
        }
    }
    // post{
    //     always{
    //         junit '**/*.dpl.xml'
    //     }
    // }
}
