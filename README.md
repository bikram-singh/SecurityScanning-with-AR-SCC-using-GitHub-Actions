# SecurityScanning-with-AR-SCC-using-GitHub-Actions
This repository is used to Automated Security Scanning with Artifact Registry + Security Command Center Using GitHub Actions


**Security Scanning Workflow Overview
What This Workflow Does**
After deploying your Docker image to Cloud Run, this workflow automatically:

Checks **Google Cloud Security Command Center (SCC)** for **vulnerability findings** related to your deployed container image.

Waits up to 3 minutes (polling every 6 seconds) for any findings.

**If no vulnerability findings are detected**, it prints:

No vulnerability findings found.
If any high or critical vulnerabilities are found, it:

Prints their details

Exits with an error (non-zero), causing the GitHub Action job to fail.

**Use Case and How to Check Results
Purpose**
Automatically scan your deployed container image in SCC to detect security vulnerabilities before marking the deployment as successful.

**Where to Check Results**
In your GitHub Actions logs, you will see either:

"No vulnerability findings found." → deployment passed security scan

Or a list of vulnerabilities and the job will fail → you should investigate and fix those before deploying or promoting.

In the Google Cloud Console under:


Security Command Center → Findings
you can view detailed reports of vulnerabilities related to your container image.

**If Vulnerabilities Exist**
The workflow calls sys.exit(1), which causes the GitHub Action job to fail.

This prevents marking the deployment as successful or can be used to halt promotion pipelines.

You can then analyze and fix vulnerabilities, rebuild the container, and redeploy.

