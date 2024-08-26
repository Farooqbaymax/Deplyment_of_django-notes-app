---

# Notes App

This is a Notes application built with React and Django, which I have forked from [Londhe Shubham's repository](https://www.youtube.com/@TrainWithShubham). The project has been Dockerized and configured with Nginx as a reverse proxy to handle traffic efficiently.

## Requirements

- **Python 3.9**
- **Node.js**
- **Docker**
- **Nginx** (for reverse proxy)

## Installation and Setup

### Clone the Repository

Start by cloning the repository:

```bash
git clone https://github.com/LondheShubham153/django-notes-app.git
cd django-notes-app
```

### Dockerize the Application

#### Build the Docker Image

To build the Docker image for the application, run the following command from the root directory of the project:

```bash
docker build -t notes-app .
```

#### Run the Docker Container

After building the Docker image, run the container with the following command:

```bash
docker run -d -p 8000:8000 notes-app:latest
```

This command will start the application and expose it on port 8000.

### Configure Nginx as a Reverse Proxy

To set up Nginx as a reverse proxy for the Dockerized application, follow these steps:

1. **Install Nginx**

   Update the package list and install Nginx:

   ```bash
   sudo apt-get update
   sudo apt install nginx
   ```

2. **Configure Nginx**

   Create a new Nginx configuration file or modify the existing one. You can add a configuration like the following:

   ```nginx
   server {
       listen 80;

       server_name your-domain.com;

       location / {
           proxy_pass http://localhost:8000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }
   }
   ```

   Save this file as `/etc/nginx/sites-available/notes-app` and create a symlink in `sites-enabled`:

   ```bash
   sudo ln -s /etc/nginx/sites-available/notes-app /etc/nginx/sites-enabled/
   ```

3. **Restart Nginx**

   To apply the new configuration, restart Nginx:

   ```bash
   sudo systemctl restart nginx
   ```

## Acknowledgements

A special thanks to [Londhe Shubham](https://www.youtube.com/@TrainWithShubham) for creating the original Notes application and providing the foundational work. His tutorials and guidance were instrumental in setting up and deploying this application.

---

Feel free to adjust any specifics according to your setup or additional features you might have implemented.
