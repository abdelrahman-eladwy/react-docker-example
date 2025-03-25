# React Docker Example

## Project Overview

This is a sample React application demonstrating how to containerize a React app using Docker and set up a CI/CD pipeline with Jenkins. The project is bootstrapped with Create React App and includes a complete setup for building, dockerizing, and deploying the application.

## Project Structure

```
react-docker-example/
│
├── public/                 # Public assets and HTML template
│   ├── index.html          # Main HTML file
│   ├── manifest.json       # Web app manifest
│   └── robots.txt          # Robots configuration
│
├── src/                    # Source code
│   ├── App.css             # Application styles
│   ├── App.js              # Main React component
│   ├── App.test.js         # Component tests
│   ├── index.js            # Entry point
│   └── ...
│
├── Dockerfile              # Docker configuration
├── Jenkinsfile             # Jenkins pipeline configuration
└── package.json            # Project dependencies and scripts
```

## Prerequisites

- Node.js (v18+)
- Docker
- Jenkins (for CI/CD)

## Local Development

### Installation

1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```

### Available Scripts

- `npm start`: Runs the app in development mode
- `npm test`: Launches the test runner
- `npm run build`: Builds the app for production

## Docker Setup

### Building the Docker Image

```bash
docker build -t react-docker-example .
```

### Running the Docker Container

```bash
docker run -p 80:80 react-docker-example
```

## CI/CD with Jenkins

The project includes a `Jenkinsfile` that defines a pipeline with three stages:

1. **Build Docker Image**: Creates a Docker image
2. **Docker Push**: Pushes the image to Docker Hub
3. **Deploy Docker Container**: Runs the container locally

### Jenkins Pipeline Steps

- Builds the Docker image with a unique tag based on the build number
- Pushes the image to Docker Hub
- Stops and removes any existing container
- Starts a new container with the latest image

## Deployment

The application is deployed using Nginx, serving the React build files from `/usr/share/nginx/html`.

## Technologies Used

- React 18
- Docker
- Nginx
- Jenkins
- Create React App

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

Distributed under the MIT License. See `LICENSE` for more information.

## Contact

Your Name - your.email@example.com

Project Link: [https://github.com/yourusername/react-docker-example](https://github.com/yourusername/react-docker-example)
