# prog1-CR

Architectural Diagram

![image](https://github.com/rudrabarot71/prog1-CR/assets/81606729/11290052-cf1c-40e8-a4d4-0e6e7ff462d2)



Services Used
AWS S3
AWS EC2 Instance
AWS SQS Messaging Service
AWS Rekognition

Steps Performed
1. AWS Learner's Lab Setup
Log in to AWS Learner's Lab using your student account.
The lab session will provide AWS credentials and display your remaining student credits.
2. AWS CLI Setup
Install AWS CLI.
Configure your credentials using aws configure.
Create multiple profiles if needed using export AWS_PROFILE=<profile_name>.
3. IAM Setup
Navigate to IAM -> Roles -> LabRole.
Ensure that the role includes necessary policies, such as AmazonRekognitionFullAccess, AmazonS3FullAccess, and AmazonSQSFullAccess.
4. EC2 Instance Configuration
Go to Services -> EC2.
Launch EC2 instances with specifications like Amazon Linux 2, t2.micro, security group settings, and storage configuration.
5. SSH Access to EC2 Instances
Download the SSH key (labsuser.pem).
Change permissions with chmod 400 labsuser.pem.
Use ssh -i labsuser.pem ec2-user@<EC2_IP> to access the instances.
Installing Oracle JDK 19.0.1 on AWS Linux AMI:

i)Download Oracle JDK
wget https://download.oracle.com/java/19/archive/jdk-19.0.1_linux-x64_bin.tar.gz

ii)Extract the files:
After downloading the JDK, extract it using the tar command:
tar -xvf jdk-19.0.1_linux-x64_bin.tar.gz

iii) Move the extracted JDK:
You can move the extracted JDK to a suitable location on your system. For example, you can move it to /usr/local:
sudo mv jdk-19.0.1 /usr/local/

iv) Update Environment Variables:
To set up environment variables, you need to create a new file for Oracle JDK in /etc/profile.d/.
sudo touch /etc/profile.d/oraclejdk.sh
sudo chmod +x /etc/profile.d/oraclejdk.sh
sudo vi /etc/profile.d/oraclejdk.sh
execute these one by one
Add the following lines to /etc/profile.d/oraclejdk.sh:
export JAVA_HOME=/usr/local/jdk-19.0.1
export PATH=$JAVA_HOME/bin:$PATH
Save the file and exit the text editor (in Vi, you can save with :wq

v) Reload shell configuration:
To apply the environment variables, either logout and log back in or run:
source /etc/profile.d/oraclejdk.sh

vi) Check Java version:
Finally, you can check the installed Java version:
java -version
This should display the version of the Oracle JDK you installed.


7. AWS SQS Configuration
Navigate to Amazon SQS and create a queue (e.g., Car.fifo).
Configure encryption, access policy, and assign it to the LabRole.
8. Java App for Image Recognition
Fetch images from the S3 bucket.
Use AWS Rekognition to find image labels and confidence scores.
Send the names of images with a "Car" label and confidence score > 90% to the AWS SQS message queue.
Send a "-1" message at the end.
9. Prepare the JAR file for deployment.
10. Java App for Text Detection
Fetch messages from the AWS SQS queue.
Use AWS Rekognition for text detection.
Write images with detected text to ImageText.txt.
11. Prepare the JAR file for deployment.
12. Java Application Deployment on EC2 Instances
SSH to the EC2 instances.
Configure AWS using aws configure.
Install openjdk-java-19.0.1.
Move JAR files to the instances.
Run the Java applications.
Both the car recognition and text detection apps can run in parallel.






