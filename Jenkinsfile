@Library('libpipelines') _

hose {
    EMAIL = 'cd'
    NEW_VERSIONING = 'true'
    BUILDTOOL = 'make'

    DEV = { config ->
        doCompile(config)
        doPackage(config)
        doDeploy(config)
        doDocker(conf: config, skipOnPR: false)
        }
}
