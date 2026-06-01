# 🖼️ AI Powered Image Analyzer

An intelligent image analysis application powered by AWS Rekognition, AWS Bedrock, Lambda, API Gateway, S3, and Terraform. Upload an image through a static web frontend and get AI-generated image labels plus a natural language description.

## 🌟 Features

- **AI Image Understanding**: Uses AWS Rekognition to detect objects, scenes, and labels from uploaded images
- **Generative Description**: Uses AWS Bedrock with the Mistral model to generate a clear sentence describing the image
- **Serverless Backend**: AWS Lambda handles image processing without managing servers
- **REST API**: API Gateway exposes a `/analyze` endpoint for the frontend
- **Static Frontend Hosting**: S3 hosts the HTML, CSS, and JavaScript frontend as a static website
- **Infrastructure as Code**: Terraform provisions AWS resources automatically
- **Automatic Frontend Upload**: Terraform uploads `frontend/index.html` to S3 using `aws_s3_object`

## 🛠️ Tech Stack

- **Infrastructure**: Terraform
- **Cloud Provider**: AWS
- **Backend**: AWS Lambda with Python 3.9
- **Image Detection**: Amazon Rekognition
- **Generative AI**: Amazon Bedrock, Mistral Small model
- **API Layer**: Amazon API Gateway
- **Frontend Hosting**: Amazon S3 Static Website Hosting
- **Frontend**: HTML, CSS, JavaScript

## 📁 Project Structure

```
Image_Analyzer_using_Bedrock_Rekognition_Terraform/
├── frontend/
│   └── index.html              # Static web frontend
├── lambda/
│   └── image_analyzer.py       # Lambda function for Rekognition + Bedrock
├── terraform/
│   ├── main.tf                 # Main Terraform infrastructure
│   ├── variables.tf            # Terraform input variables
│   ├── outputs.tf              # Terraform output values
│   └── .terraform.lock.hcl     # Provider dependency lock file
├── .gitignore                  # Ignores Terraform state/cache and local files
└── README.md                   # Project documentation
```

## 🚀 Getting Started

### Prerequisites

- AWS account
- AWS CLI configured with valid credentials
- Terraform installed
- Bedrock model access enabled in your AWS region
- IAM permissions for Lambda, API Gateway, S3, Rekognition, Bedrock, IAM, and CloudWatch Logs

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/deep1305/AI_Powered_Image_Analyzer_using_Terraform_Rekognizer_Bedrock.git
   cd "Image_Analyzer_using_Bedrock_Rekognition_Terraform"
   ```

2. **Go to the Terraform folder**
   ```bash
   cd terraform
   ```

3. **Initialize Terraform**
   ```bash
   terraform init
   ```

4. **Review the deployment plan**
   ```bash
   terraform plan
   ```

5. **Deploy the infrastructure**
   ```bash
   terraform apply
   ```

6. **Copy the API Gateway URL**

   After deployment, Terraform prints `api_gateway_url`. Add `/analyze` at the end of that URL.

   Example:
   ```text
   https://your-api-id.execute-api.us-east-1.amazonaws.com/v1/analyze
   ```

7. **Update the frontend API endpoint**

   Open `frontend/index.html` and update:
   ```javascript
   const API_ENDPOINT = 'https://your-api-id.execute-api.us-east-1.amazonaws.com/v1/analyze';
   ```

8. **Apply Terraform again**

   Terraform automatically uploads the updated `index.html` to the S3 website bucket.
   ```bash
   terraform apply
   ```

9. **Open the frontend website**

   Use the `frontend_website_endpoint` output from Terraform to open the deployed app in your browser.

## 💡 Usage

1. Open the S3 frontend website URL
2. Upload an image
3. Click the analyze button
4. The frontend sends the image to API Gateway
5. Lambda sends the image to Rekognition
6. Rekognition returns detected labels
7. Bedrock generates a natural English description
8. The frontend displays the labels and AI-generated description

## 📊 How It Works

1. **User Uploads Image**: The browser converts the uploaded image into base64
2. **API Gateway Receives Request**: The frontend sends a POST request to `/analyze`
3. **Lambda Processes Image**: Lambda decodes the image and sends it to Rekognition
4. **Rekognition Detects Labels**: AWS Rekognition returns labels such as objects, scenes, and concepts
5. **Bedrock Generates Description**: Lambda sends the labels to Bedrock and asks for one natural sentence
6. **Response Goes Back to Frontend**: The browser displays the detected labels and generated description

## 🌐 Terraform Resources

This project creates:

- IAM role and policies for Lambda
- Lambda function package from the `lambda/` folder
- API Gateway REST API with POST and OPTIONS methods
- Lambda permission for API Gateway invocation
- S3 bucket for frontend static website hosting
- S3 bucket website configuration
- S3 bucket policy for public website access
- S3 object upload for `frontend/index.html`

## 🧹 Cleanup

To delete the AWS resources created by this project:

```bash
cd terraform
terraform destroy
```

## 🙏 Acknowledgments

- Built with AWS Rekognition for image label detection
- Powered by AWS Bedrock for generative AI descriptions
- Deployed using Terraform infrastructure as code

---

**Made with ❤️ for cloud and AI builders**
