pipeline {
    agent any
    // pipeline내에서 사용할 변수 를 설정할 수 있다. enviroment와 비슷함
    parameters {
        // string 형태의 변수를 선언
        string(
            // 변수명을 'COPY_SOURCE_PROJECT'
            name: 'COPY_SOURCE_PROJECT',
            // 기본값으로 "PipelineTest04"를 지정
            defaultValue: "PipelineTest04",
            // 변수의 설명을 지정
            description: 'Name of source project for copying of artifacts.'
        )
    }
    stages {
        stage('delete workspace') {
            steps {
                //기존의 workspace를 정리합니다.
                deleteDir()
            }
        }
        stage('copy artifacts') {
            steps {
                // PipelineTest04의 파일을 복사합니다.
                copyArtifacts(projectName:"${params.COPY_SOURCE_PROJECT}")
            }
        }
        stage('find files') {
            steps {
                // 그루비를 사용합니다.
                script{
                    //files라는 변수에 findFiles라는 내장함수로 파일목록을 가져옵니다.
                    files = findFiles(glob: '*.*')
                    // 반복하여 파일 목록을 출력합니다.
                    for ( file in files ){
                        echo file.name
                    }
                }
            }
        }
    }
}
