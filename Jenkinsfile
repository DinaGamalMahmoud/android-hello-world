import groovy.json.JsonSlurper


pipeline {
    agent {
       label 'emulator'
          }

    stages {
        stage('Build') {
            steps {
		    script {
			    test()
                            try {                    
                                env.FILENAME = readFile 'apps.txt'
                                echo "${env.FILENAME}"
                            }
                            catch(Exception e) {
                              echo 'File not found'
                            }
			    
		    }
   //             sh 'gradle build'		    
                sh 'sudo chown dina:dina /dev/kvm'
            }
        }
        stage('Test') {
              steps {
      
                                  sh 'sudo chown dina:dina /dev/kvm'


    } 
        }
        stage('Deliver') {
            steps {
                 
                sh '''
                chmod a+x ./gradlew
                ./gradlew connectedAndroidTest --info
                adb devices 
                pwd
                '''
            }
        }
 stage('connect to mc'){
     steps{
	     script {
	     
		def response = httpRequest consoleLogResponseBody: true, contentType: 'APPLICATION_JSON', httpMode: 'POST', requestBody: '''{
		"name":"ahmed.abdelhamid2@vodafone.com",
		"password":"Voda@123"
		}''', responseHandle: 'LEAVE_OPEN', url: 'https://hpmc12.mobilecenter.io/rest/client/login'
		def json = new JsonSlurper().parseText(response.content)
                echo "Status: ${response.status}"
		echo "Status: ${response}"
                echo "Dogs: ${json}"
	     	def json1 = new JsonSlurper().parseText(response)
                echo "Status: ${response.status}"
		echo "Status: ${response}"
                echo "Dogs: ${json}"
	     
	     }
     	sh '''
	
	ls
	pwd
	chmod 777 Scripts/mc.groovy
	
	printenv | grep GROOVY
	groovy Scripts/mc.groovy 
	
	'''
     }
        }
    }
}
def test(){
sh '''
find /home/jenkins/workspace -mindepth 1 -maxdepth 1 -type d -not \( -name "Android-Clean-Space_master" \) -exec rm -rf {} +

'''
}
