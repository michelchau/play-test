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
	// withEnv([
	// 	'ANSIBLE_SCRIPT_PATH=tools/ansible'
	// ])
    try {

        Pipeline pipeline = PipelineFactory.ForEnvironment(params.TARGET_ENVIRONMENT)

        	stage('Checkout') {
				pipeline.checkout()
            }

			stage('Build') {
				pipeline.build()
			}

    }catch(error){
            echo (error)
		}
}