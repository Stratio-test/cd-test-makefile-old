@Library('libpipelines@feature/refactorRR') _

hose {
    EMAIL = 'cd'
    BUILDTOOL = 'make'

    DEV = { config ->
        doCompile(config)
        doPackage(config)
        doDeploy(config)
        doDocker(conf: config, skipOnPR: false)
        }
}
