pipeline {
    agent any

    stages {
        stage ('EmailApproval'){
        
                    //def jobName = currentBuild.fullDisplayName
            environment{
                    def mailToRecipients = "bansal.mitesh6@gmail.com"
                    def useremail = "bansal.mitesh@gmail.com"
                    def user = "bansal,mitesh"
                    def userAborted = false
            }
            steps{
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
            
  
        stage('Hello') {
            steps {
                sh ''' cat /etc/os-release'''
            }
        }
    }
}
