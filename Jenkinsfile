pipeline {
  agent any

  triggers {
    githubPush()
  }

  options {
    disableConcurrentBuilds()
    timestamps()
  }

  environment {
    HPC_HOST = 'batch.ncifcrf.gov'
    HPC_USER = 'xies4'
    HPC_DIR  = '~/test_jenkins'
    SSH_CREDENTIALS_ID = 'FSGCIFX'
  }

  stages {
    stage('Checkout') {
      when { branch 'main' }
      steps {
        checkout scm
      }
    }

    stage('Submit HPC job') {
      when { branch 'main' }
      steps {
        sshagent(credentials: [env.SSH_CREDENTIALS_ID]) {
          script {
            def shortCommit = env.GIT_COMMIT.take(7)

            sh """
              set -euo pipefail

              ssh -o BatchMode=yes -o StrictHostKeyChecking=no ${env.HPC_USER}@${env.HPC_HOST} 'mkdir -p ${env.HPC_DIR}'

              cat > job.sh <<'EOF'
#!/bin/bash
#SBATCH --partition=norm
#SBATCH --job-name=test_commit
#SBATCH --output=slurm-%j.out
#SBATCH --error=slurm-%j.err
#SBATCH --time=00:05:00
#SBATCH --cpus-per-task=1
#SBATCH --mem=1G

set -euo pipefail
mkdir -p ${env.HPC_DIR}/
touch ${env.HPC_DIR}/test.${shortCommit}.txt
EOF

              scp -o BatchMode=yes -o StrictHostKeyChecking=no job.sh ${env.HPC_USER}@${env.HPC_HOST}:${env.HPC_DIR}/job.sh

              ssh -o BatchMode=yes -o StrictHostKeyChecking=no ${env.HPC_USER}@${env.HPC_HOST} '
                cd ${env.HPC_DIR} &&
                sbatch job.sh
              '
            """
          }
        }
      }
    }
  }
}