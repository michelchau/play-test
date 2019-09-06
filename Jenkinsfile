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
				string(
					defaultValue: 'project-name',
					description: 'play-test',
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