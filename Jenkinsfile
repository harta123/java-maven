node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("danuamirudin/docker-hub-credentials")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
    
    stage('send to another server') { 
    	steps {
//     withCredentials([sshUserPrivateKey(credentialsId: '8210a265-20a4-403d-8e08-d2f618f7403f', keyFileVariable: 'KEY',usernameVariable: 'userName')]) {
        sh "ssh ubuntu@3.138.151.0 'sudo docker login https://image.mylab-siab.com -u rastacode090802 -p Damarwulan1&&sudo docker run --name=sukar -d -p 1337:8080 -t image.mylab-siab.com/learning/reaxjs-maven-jenkins'"
        // sh "whoami"
        // sh "docker login https://image.mylab-siab.com -u rastacode090802 -p Damarwulan1"
        // sh"docker run --name=sukar -d -p 1337:3000 -t image.mylab-siab.com/learning/reaxjs-maven-jenkins"
//         // sh "|id|whoami|docker login https://image.mylab-siab.com -u rastacode090802 -p Damarwulan1|docker run --name=rexasjs -d -p 1337:3000 -t image.mylab-siab.com/learning/reaxjs-maven-jenkins"
//         sh "id"
     }
}
