@Library('Prismic')
import org.prismic.pipeline.Script
import org.prismic.pipeline.Pipeline
import org.prismic.pipeline.Environment
import org.prismic.pipeline.PipelineFactory
node ('master'){

    Script.environment = this

	properties([
		parameters(
			[
				choice(
					choices: Environment.getEnvironmentsList(),
					description: 'Please enter the environment',
					name: 'TARGET_ENVIRONMENT'
				),
				choice(
					choices: Environment.getClusterList(),
					description: 'Please choose your cluster',
					name: 'TARGET_CLUSTER'
				),


				booleanParam(
					defaultValue: false,
					description: 'Do you want to build ?',
					name: 'BUILD'
				),
				string(
					defaultValue: '',
					description: 'APP version',
					name: 'APP_VERSION'
				),
				string(
					defaultValue: 'play-test',
					description: 'project-name',
					name: 'PROJECT_NAME'
				),

				string(
					defaultValue: 'git@github.com:michelchau/play-test.git',
					description: 'Repo url',
					name: 'GIT_URL'
				)
            ]
        )
    ])


	withEnv([
		'ANSIBLE_SCRIPT_PATH=tools/ansible'
	]){

    try {

        Pipeline pipeline = PipelineFactory.ForEnvironment(params.TARGET_ENVIRONMENT)

        	stage('Checkout') {
				pipeline.checkout()
				steps{
					echo "test"
				}
            }

			env.releaseVersion = pipeline.getReleaseVersion();
			echo 'The release version is: ' + env.releaseVersion

			stage('Build') {
				if(params.BUILD)
				pipeline.build()
			}
			stage ('Deploy') {
				pipeline.deploy()
			}

    }catch(error){
            echo (error)
		}
	}
}