# shell-scripting-project1

This shell script integrates with the GitHub API to list users who have access to a specified GitHub repository. It's a practical tool for DevOps engineers to monitor repository access programmatically, especially useful for tasks like auditing permissions when someone leaves the organization.

The script fetches repository collaborator information, focusing on non-admin users (those with pull permissions but admin set to false) to identify developers or collaborators with read/write access.

Prerequisites
Before running this script, ensure you have the following installed on your Linux environment (e.g., an EC2 instance as demonstrated in the video):

Git: To clone the repository containing the script.
JQ: A lightweight and flexible command-line JSON processor.
Curl: A command-line tool for transferring data with URLs (usually pre-installed).
Setup and Installation
Follow these steps to set up and run the script:

1. Launch an EC2 Instance (Optional, but recommended for demonstration)
As demonstrated in the video, you can launch a fresh Ubuntu EC2 instance on AWS:

Go to the AWS EC2 console.
Click "Launch instance."
Name your instance (e.g., "shell-script-example").
Select "Ubuntu" as the AMI.
Choose your key pair and launch the instance.
Once the instance is running, copy its Public IPv4 address.
Open your terminal and SSH into the instance: bash ssh -i "your-key.pem" ubuntu@
2. Clone the Script Repository
On your EC2 instance (or local machine), clone the repository containing the script:

bash
git clone https://github.com/iam-veeramalla/shell-scripting-projects.git

Navigate into the script's directory:

bash
cd shell-scripting-projects/github-api

3. Install JQ
JQ is essential for parsing the JSON output from the GitHub API. Install it using apt:

bash
sudo apt install JQ -y

4. Obtain a GitHub Personal Access Token
To authenticate with the GitHub API, you'll need a Personal Access Token (PAT).

Go to [github.com]https://github.com.
Click on your profile picture in the top right corner.
Select Settings.
In the left sidebar, scroll down and click Developer settings.
Click Personal access tokens, then select Tokens (classic).
Click Generate new token.
Note: Give your token a descriptive name 
Grant appropriate permissions: For this script, you'll need at least repo permissions to read repository information. Be cautious with the permissions you grant, especially delete or admin access, as this token will have the same capabilities as your user account.
Click Generate token.
Crucially, copy the generated token immediately! It will only be shown once.
5. Export Environment Variables
Before running the script, export your GitHub username and the copied Personal Access Token as environment variables. This keeps sensitive information out of the script itself.

Replace and with your actual credentials:

bash
export USERNAME=""
export TOKEN=""

6. Grant Script Execution Permissions
Make the script executable:

bash
chmod 777 list-users.sh

(Note: 777 grants full permissions for simplicity in demonstration; in a production environment, you might use more restrictive permissions like 755.)

Execution
To run the script, provide the organization name (or your GitHub username for personal repositories) and the repository name as command-line arguments:

bash
./list-users.sh

Example:

To list users for the python repository within the devops-by-examples organization:

bash
./list-users.sh devops-by-examples python

The script will then output the login names of the collaborators who have access to the specified repository. If you attempt to query a repository you don't have sufficient access to view collaborator settings, the script will likely return an error.
