# AWS Automated CodeCommit Backup to S3

CloudFormation Template for performing automated backups of CodeCommit repositories to S3.

This CloudFormation Template is based on the architecture detailed in AWS Prescriptive Guidance Patterns: [Automate event-driven backups from CodeCommit to Amazon S3 using CodeBuild and CloudWatch Events](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/automate-event-driven-backups-from-codecommit-to-amazon-s3-using-codebuild-and-cloudwatch-events.html).

## Summary
- On the Amazon Web Services (AWS) Cloud, you can use AWS CodeCommit to host secure Git-based repositories. CodeCommit is a fully managed source control service. However, if a CodeCommit repository is accidentally deleted, its contents are also deleted and cannot be restored. 

- This pattern describes how to automatically back up a CodeCommit repository to an Amazon Simple Storage Service (Amazon S3) bucket after a change is made to the repository. If the CodeCommit repository is later deleted, this backup strategy provides you with a point-in-time recovery option.

## Templates

- `codecommit_repository.yml` : Simple CloudFormation Template for creating a CodeCommit Repository.
- `codecommit_automated-backup.yml` : CloudFormation Template for automated CodeCommit Repository backup solution, creates EventBridge rules, CodeBuild Project, S3 Storage bucket .etc

## Architecture
1. Code is pushed to a CodeCommit repository.
2. The CodeCommit repository notifies CloudWatch Events of a repository change (for example, a git push command).
3. CloudWatch Events invokes AWS CodeBuild and sends it the CodeCommit repository information.
4. CodeBuild clones the entire CodeCommit repository and packages it into a .zip file.
5. CodeBuild uploads the .zip file to an S3 bucket.

![Screenshot](images/ddd61eb9-bcf7-42db-a1ab-4f695d038349.png?raw=true)

