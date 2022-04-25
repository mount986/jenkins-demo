podTemplate(containers: [containerTemplate(name: 'jruby', image: 'jruby:9.2', ttyEnabled: true, command: 'cat',
                         envVars: [envVar(key: 'JAVA_OPTS', value: "-Xms512m -Xmx1024m")])])
                         
{
    node(POD_LABEL) {
        stage ('Test'){
            container('jruby'){
                stage('check the version'){
                    sh "jruby -v"
                }
            }
        }
    }
}