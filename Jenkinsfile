def changelog(){
  withCredentials([usernamePassword(credentialsId: 'jenkinsCredentials', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {    
    bat"curl -u ${USERNAME}:${PASSWORD} ${env.BUILD_URL}/api/xml?xpath=/*/changeSet -o file.xml"
        def file = readFile(file: "file.xml") 
        print(file)
        def msg = "Changes deployed through the build:"  
        if(file != "XPath /*/changeSet didn?t match"){  
                    def response = new XmlSlurper().parseText(file) 
                    for(int i=0;i<response.item.size(); i++){
                        def z= i+1
                        msg =  msg + "\n" + "${z}" + ". "  + response.item[i].msg    
                    }
        }else{
                msg = " No commits"
            } 
        return msg  
  } 
}


node{
 
  try {
  
    stage("check"){
        
        v = "origin/release-sprint-22"

        
    }
    stage('commiting'){
         
        
          
              
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sumitbhardwajji/new.git']]])
             
              bat"   git config --global user.name \"sumitbhardwajji\" "
              bat"   git config --global user.email \"sumitbhardwa7303@gmail.com\" "
              bat "git checkout $branch"
              bat"   echo 'testing sumit bhardwajji ffffhsh great hello sfdf ' > sumit2.txt "
              bat "git status"
             // bat "ls | cat sumit2.txt"
              bat"   git add . "
              bat"   git commit -m \"intial\" "
              def l = env.Branch.tokenize("/")
              l = l[1]
              def pass= "Ramnagartanda@84"
      bat" git push https://sumitbhardwajji:${pass}@github.com/sumitbhardwajji/new.git HEAD:refs/heads/$l "
             
          checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sumitbhardwajji/notejam.git']]])


            
      
        }
            stage("success notification "){
                def change=changelog()
                slackSend color: "#00FF00", message: "Build Successful: ${change}"              
            }
    
    
  }catch(error){
    stage("error"){
          def change=changelog()
          slackSend color: "#00FF00", message: "Build Successful: ${change}"
           
    }
  }
}
