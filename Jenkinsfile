pipeline {
    agent any

    stages {
        stage ('EmailApproval'){
        
                    
            
            steps{
                script{
                    def jobName = currentBuild.fullDisplayName
            
                    def mailToRecipients = "bansal.mitesh@gmail.com"
                    def useremail = "bansal.mitesh@gmail.com"
                    def user = "bansal,mitesh"
                    def userAborted = false
                emailext body: '''
                        Please go to console output of ${BUILD_URL}input to approve or Reject.<br>
                    ''',    
                        mimeType: 'text/html',
                        subject: "[Jenkins] ${JOB_NAME} Build Approval Request",
                        from: "${useremail}",
                        to: "${mailToRecipients}",
                        recipientProviders: [[$class: 'CulpritsRecipientProvider']]

                    try { 
                        userInput = input submitter: "${user}", message: 'Do you approve?'
                    } catch (org.jenkinsci.plugins.workflow.steps.FlowInterruptedException e) {
                    cause = e.causes.get(0)
                    echo "Aborted by " + cause.getUser().toString()
                    userAborted = true
                        echo "SYSTEM aborted, but looks like timeout period didn't complete. Aborting."
                        error('Deployment not approved')
                    }
            }
        }
        }    
  
        stage('Hello') {
            steps {
                sh ''' cat /etc/os-release'''
            }
        }
     }
    post {
    success {
      emailext to:"bansal.mitesh@gmail.com", subject:"SUCCESS: ${currentBuild.fullDisplayName}", body: "Yay, we passed."
 }
}

