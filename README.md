# Jenkins Pipeline Test Application

A simple Node.js Express application designed to test Jenkins CI/CD pipeline with GitHub webhooks.

## Features

- Express.js REST API
- Unit tests with Jest
- ESLint code quality checks
- Docker containerization
- Jenkins pipeline configuration

## API Endpoints

- `GET /` - Welcome message with timestamp
- `GET /health` - Health check endpoint
- `GET /api/users` - Sample users data

## Local Development

```bash
# Install dependencies
npm install

# Run the application
npm start

# Run tests
npm test

# Run linting
npm run lint
```

## Jenkins Pipeline

The `Jenkinsfile` includes the following stages:

1. **Checkout** - Pull code from GitHub
2. **Setup Node.js** - Verify Node.js environment
3. **Install Dependencies** - Run `npm install`
4. **Lint Code** - Run ESLint for code quality
5. **Run Tests** - Execute Jest unit tests
6. **Build** - Create build artifacts
7. **Deploy to Staging** - Deploy on main branch
8. **Health Check** - Verify deployment

## Docker

```bash
# Build image
docker build -t jenkins-pipeline-test .

# Run container
docker run -p 3000:3000 jenkins-pipeline-test
```

## Testing Your Jenkins Setup

1. Push this code to your GitHub repository
2. Ensure webhook is configured to trigger Jenkins
3. Make a commit to trigger the pipeline
4. Monitor Jenkins console output for each stage
5. Verify all stages pass successfully

## Pipeline Testing Scenarios

- **Success Path**: All tests pass, code quality checks pass
- **Test Failure**: Modify tests to fail and observe pipeline behavior
- **Lint Failure**: Introduce code quality issues
- **Build Failure**: Break the application code

This application provides a comprehensive test for your Jenkins master-slave setup with GitHub integration.