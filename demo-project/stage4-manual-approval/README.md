# Stage 4: Manual Approval Pipeline

## 🎯 Learning Goal
Demonstrate environment-specific deployments with manual approval for production.

## 🚀 Deploy This Stage

### Via Pipeline (Recommended)
```bash
# Update demo-config.txt and push to trigger pipeline
echo "stage4-manual-approval" > demo-config.txt
git add demo-config.txt
git commit -m "Deploy Stage 4: Manual approval workflow"
git push
```

### Manual Deployment Options

#### Test Environment
```bash
# Prerequisites auto-created by pipeline infrastructure
cd demo-project/stage4-manual-approval
terraform init
terraform apply -var="environment=test"
```

#### Production Environment
```bash
terraform apply -var="environment=prod"
```

## 🎨 Visual Differences

### Test Environment
- **Background**: Teal/Green (#4ecdc4)
- **Header**: "🧪 TEST"
- **Instance**: t2.micro
- **Message**: "✅ Safe to experiment"

### Production Environment  
- **Background**: Red (#ff6b6b)
- **Header**: "🚨 PRODUCTION 🚨"
- **Instance**: t2.small
- **Message**: "⚠️ Handle with care!"

## 🎤 Speaker Talking Points

### Before Deployment
*"In real-world scenarios, you need different configurations for test and production environments, plus approval workflows for production changes."*

### Setup Phase
*"Notice how we create separate Parameter Store paths and Secrets Manager secrets for each environment. This ensures complete isolation."*

### Test Deployment
*"Test deployments are automatic - developers can deploy freely to validate changes."*

### Production Deployment
*"Production requires manual approval. In a real pipeline, this would pause and send notifications to approvers."*

## 🔍 Key Teaching Moments

### 1. Environment Separation
- **Parameter Store**: `/demo/test/` vs `/demo/prod/`
- **Secrets Manager**: `demo/test/api-key` vs `demo/prod/api-key`
- **Instance Types**: t2.micro (test) vs t2.small (prod)

### 2. Approval Workflows
- **Test**: Automatic deployment
- **Production**: Manual approval required
- **Visual Feedback**: Different colors and warnings

### 3. Configuration Management
- **Environment-specific**: Different API endpoints
- **Security**: Separate secrets per environment
- **Validation**: Terraform validates environment values

## 🔄 Pipeline Behavior
- ✅ Test deploys automatically
- ⏸️ Production waits for approval (in full pipeline)
- 🎨 Visual distinction between environments
- 🔒 Environment-specific secrets
- ✅ Prerequisites auto-created by pipeline infrastructure
- 📍 State stored: `anthony-terraform-tfstate/automating-terraform-with-aws-codepipeline/stage4/`

## 🎯 Production Pipeline Integration
In a real CodePipeline, this would include:
- Manual approval action before production deployment
- SNS notifications to approvers
- Different IAM roles per environment
- Separate S3 buckets for state files

## 🧹 Cleanup
```bash
# Destroy test environment
terraform destroy -var="environment=test"

# Destroy production environment  
terraform destroy -var="environment=prod"
```