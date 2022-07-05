// see https://dzone.com/refcardz/continuous-delivery-with-jenkins-workflow for tutorial
// see https://documentation.cloudbees.com/docs/cookbook/_pipeline_dsl_keywords.html for dsl reference
// This Jenkinsfile should simulate a minimal Jenkins pipeline and can serve as a starting point.
// NOTE: sleep commands are solelely inserted for the purpose of simulating long running tasks when you run the pipeline
node {
   stage 'deploy Canary'
   sh 'echo "Application fait sur Jenkinsfile"; sleep 5;'

   stage 'deploy Production'
   input 'Proceed?'
   sh 'echo "Application fait sur Jenkinsfile"; sleep 6;'
}
