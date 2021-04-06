import java.text.SimpleDateFormat

@Library('libpipelines@master') _

hose {
    EMAIL = 'cd'
    BUILDTOOL = 'make'
    REPOSITORYLESS_BUILD = true
    DEBUG = true

    NEW_VERSIONING = true
    //FREESTYLE_BRANCHING = true

    DOCKERFILE = """FROM ubuntu:16.04
MAINTAINER QA "qa@stratio.com"

ARG VERSION

CMD ["tail -f /dev/null"]"""

    DEV = { config, currentBuild, params ->
	//currentBuild.description = params?.NEXT_VERSION
	def ROLLING_RELEASE = false
	if (params?.ROLLING_RELEASE) {
            ROLLING_RELEASE = params?.ROLLING_RELEASE.toBoolean()
        }
        if (ROLLING_RELEASE) {
            def df = new SimpleDateFormat("yyyyMMdd")
            config.INTERNAL_VERSION = "50.04-${df.format(new Date())}"
        } else {
            config.INTERNAL_VERSION = '50.04'
        }
	node (config.AGENT) {
		dir (config.INTERNAL_WORKSPACE) {
			writeFile file: 'Dockerfile', text: config.DOCKERFILE.stripMargin().stripIndent()
		}
	}
        doDocker(conf: config, skipOnPR: false)
        }
}
