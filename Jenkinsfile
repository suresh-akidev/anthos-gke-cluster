/**
 * Copyright 2020 Google LLC
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

pipeline {
  agent any
  tools {
		terraform 'terraform-14'
	}
  stages {
    stage('Set kpt and Kustomize path') {
      steps {
          sh '''
          export WORK_DIR=$PWD
          export PATH=$PATH:$WORK_DIR/bin:
          '''
      }
    }
    // [START tf-init, tf-validate]
    stage('TF init & validate') {
      when { branch "prod";branch "dev";changeRequest() }
      steps {
          sh '''
          if [[ $CHANGE_TARGET ]]; then
            TARGET_ENV=$CHANGE_TARGET
          else
            TARGET_ENV=$BRANCH_NAME
          fi
          echo ""
          echo "*************** TERRAFOM INIT and VALIDATE ******************"
          echo "******* At environment: ${env} ********"
          echo "******* At Target : ${CHANGE_TARGET} ********"
          echo "*************************************************"
          terraform init || exit 1
         
            
          '''
      }
    }
    // [END tf-init, tf-validate]

  }
}
