pipeline {
  agent any
  stages {
    stage('Tests') {
      steps {
        sh 'python2.7 hydra-report.py  /home/hydra/torque/accounting/$(date -d "2 month ago" "+%Y%m")??'
      }
    }
    stage('Build') {
      when {
        branch 'master'
      }
      steps {
        echo 'Build 6 month'
        sh '''
              python2.7 hydra-report.py  /home/hydra/torque/accounting/$(date -d "2 month ago" "+%Y%m")??
              python2.7 hydra-report.py  /home/hydra/torque/accounting/$(date -d "3 month ago" "+%Y%m")??
              python2.7 hydra-report.py  /home/hydra/torque/accounting/$(date -d "4 month ago" "+%Y%m")??
              python2.7 hydra-report.py  /home/hydra/torque/accounting/$(date -d "5 month ago" "+%Y%m")??
              python2.7 hydra-report.py  /home/hydra/torque/accounting/$(date -d "6 month ago" "+%Y%m")??'''
      }
    }
    stage('Deploy') {
      when {
        branch 'master'
      }
      steps {
        sh '''pwd
        mkdir -p /home/hydra/reports/users/monthly
        
cp -r report/assets/ /home/hydra/reports/users/monthly/assets/

cp -r report/$(date -d "2 month ago" "+%Y%m")/ /home/hydra/reports/users/monthly/$(date -d "2 month ago" "+%Y%m")/
cp report/$(date -d "2 month ago" "+%Y%m").html /home/hydra/reports/users/monthly/$(date -d "2 month ago" "+%Y%m").html


cp -r report/$(date -d "3 month ago" "+%Y%m")/ /home/hydra/reports/users/monthly/$(date -d "3 month ago" "+%Y%m")/
cp report/$(date -d "3 month ago" "+%Y%m").html /home/hydra/reports/users/monthly/$(date -d "3 month ago" "+%Y%m").html


cp -r report/$(date -d "4 month ago" "+%Y%m")/ /home/hydra/reports/users/monthly/$(date -d "4 month ago" "+%Y%m")/
cp report/$(date -d "4 month ago" "+%Y%m").html /home/hydra/reports/users/monthly/$(date -d "4 month ago" "+%Y%m").html


cp -r report/$(date -d "5 month ago" "+%Y%m")/ /home/hydra/reports/users/monthly/$(date -d "5 month ago" "+%Y%m")/
cp report/$(date -d "5 month ago" "+%Y%m").html /home/hydra/reports/users/monthly/$(date -d "5 month ago" "+%Y%m").html


cp -r report/$(date -d "6 month ago" "+%Y%m")/ /home/hydra/reports/users/monthly/$(date -d "6 month ago" "+%Y%m")/
cp report/$(date -d "6 month ago" "+%Y%m").html /home/hydra/reports/users/monthly/$(date -d "6 month ago" "+%Y%m").html

rm -rf /home/hydra/reports/users/monthly/$(date -d "7 month ago" "+%Y%m")/
rm -rf /home/hydra/reports/users/monthly/$(date -d "7 month ago" "+%Y%m").html




command_mail=$( python2.7 hydra-report.py -m config.json /home/hydra/torque/accounting/$(date -d "1 month ago" "+%Y%m")??  )


if [ -d home/hydra/reports/users/monthly/$(date -d "1 month ago" "+%Y%m")/ ]
then
   python2.7 hydra-report.py /home/hydra/torque/accounting/$(date -d "1 month ago" "+%Y%m")??
   echo "report recreate"
else
   if [[ $command_mail -ne 0 ]]
   then
   echo "Mail send"
   else
    echo "Mail error"
    python2.7 hydra-report.py /home/hydra/torque/accounting/$(date -d "1 month ago" "+%Y%m")??
    echo "Report just create"
   fi   
fi 


cp -r report/$(date -d "1 month ago" "+%Y%m")/ /home/hydra/reports/users/monthly/$(date -d "1 month ago" "+%Y%m")/
cp report/$(date -d "1 month ago" "+%Y%m").html /home/hydra/reports/users/monthly/$(date -d "1 month ago" "+%Y%m").html

'''
      }
    }
  }
}
