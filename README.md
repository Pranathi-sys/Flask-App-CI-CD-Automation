# 🚀 Flask App CI/CD Automation 🚀

Welcome to the **Flask App CI/CD Pipeline Automation** project!  
This project is a showcase of cloud-native awesomeness: a simple Flask app, containerized with Docker, seamlessly pushed to AWS Elastic Container Registry (ECR), and dynamically deployed on AWS Elastic Container Service (ECS)—all orchestrated through a fully automated Jenkins pipeline.  

---

## 🗂️ Project Overview  

### **Key Ingredients**  
- **`app.py`**: The heart of the project—a Python-powered Flask app serving "Hello, World!" goodness.  
- **`test-app.py`**: Our diligent quality assurance buddy with unit tests to ensure the `/` endpoint is flawless.  
- **`Dockerfile`**: The recipe to bake our app into a lightweight, shippable container.  
- **`.gitignore`**: Keeps the clutter (and secrets) out of your Git history.  
- **`Jenkinsfile`**: The maestro orchestrating the CI/CD symphony.

---

## 🛠️ Getting Started  

Ready to dive in? Follow these steps to get your Flask app running locally and in the cloud.  

### **Prerequisites**  
Ensure you have these tools and services at your disposal:  
1. Python 3.9+  
2. Docker  
3. AWS CLI  
4. Jenkins  
5. An AWS ECR repository and ECS cluster.

### **Run Locally**  

# Steps to Run Your Flask App

1. **Install Dependencies:**

   ```bash
   pip install -r requirements.txt
   ```
   
2. **Start the Flask app:**
```bash
Copy code
python app.py
```
3. **Open your browser and visit http://localhost:5000.**
🎉 Boom! Your Flask app is live.

### ** 🧪 Testing**
Keep your app pristine with our trusty unit tests. Run them like this:

bash
Copy code
python -m unittest discover -s . -p '*_test.py'
🐳 Docker: Containerize All the Things
Build the Image
bash
Copy code
docker build -t flask-app .
Run the Container
bash
Copy code
docker run -p 5000:5000 flask-app
Push to AWS ECR
Authenticate with AWS ECR:
bash
Copy code
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com
Tag and push the image:
bash
Copy code
docker tag flask-app:latest <account-id>.dkr.ecr.us-east-1.amazonaws.com/flask-app:latest
docker push <account-id>.dkr.ecr.us-east-1.amazonaws.com/flask-app:latest
🛠️ CI/CD Pipeline: From Code to Cloud
The CI/CD pipeline is powered by Jenkins and comprises four stages:

🎨 Build Docker Image
Build a Docker image for the Flask app.

🔐 Login to AWS ECR
Authenticate securely with AWS Elastic Container Registry.

🏷️ Tag & Push Docker Image
Tag the built image and push it to AWS ECR.

🚀 Deploy to ECS
Update the ECS service to use the latest Docker image.

Set It Up in Jenkins
Create a new Jenkins pipeline job.
Connect it to this repository.
Add your AWS credentials in Jenkins.
Run the pipeline and watch your app take flight!
🌟 Features
Simple REST Endpoint

/: Returns "Hello, World!" (because simplicity is beautiful).
Optional: Add a /health endpoint for health monitoring:

python
Copy code
@app.route('/health')
def health_check():
    return 'Healthy', 200
📈 Future Improvements
Add environment-specific configurations (staging, production).
Implement dynamic tagging for Docker images (e.g., Git commit hash).
Expand test coverage with integration tests.
Optimize security using non-root users in Docker.
