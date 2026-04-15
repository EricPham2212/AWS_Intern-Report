---
title: "Clean up resources"
weight: 9
chapter: false
pre: " <b> 4.9. </b> "
---

# Clean up resources

After completing the deployment and testing of the **AnTiScaQ** system (or finishing the Workshop exercises), the final and extremely important administrative step is **Resource Cleanup**. Accidentally leaving cloud services running in the background when they are no longer needed will lead to unexpected costs on AWS.

In this section, we will perform a **secure removal and thorough cleanup of the entire AWS infrastructure ecosystem** allocated to the project, including:

- **Computing & Applications (Elastic Beanstalk, ECR):**  
  Completely terminate the backend environment and delete the application’s Docker image repositories.

- **Storage & Data (RDS, S3):**  
  Permanently delete the MySQL relational database (without creating a final backup) and clean up the frontend/static resource storage buckets.

- **Network & Distribution (VPC, CloudFront):**  
  Disable the global content delivery network and remove the application’s internal virtual network infrastructure.

- **Monitoring (CloudWatch):**  
  Clean up and remove established automatic alarm streams.