# CeleryTestApp
CeleryTestApp is a Django application that utilizes Docker Compose with Celery, Redis, and PostgreSQL. This application demonstrates how to integrate Celery, Redis, and PostgreSQL into a Django project for asynchronous task execution.

## Prerequisites
Before running CeleryTestApp, make sure you have the following installed on your system:

Docker
Docker Compose

## Installation
To set up and run CeleryTestApp, follow these steps:
1. Clone the repository:
```
git clone https://github.com/your-username/CeleryTestApp.git
cd CeleryTestApp
```
2. Create a new Django project inside the src directory using Docker Compose:
```
docker-compose run web django-admin startproject your_project .
```
3. Update the database settings in src/your_project/settings.py to use the PostgreSQL database:
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'your_database',
        'USER': 'your_username',
        'PASSWORD': 'your_password',
        'HOST': 'db',
        'PORT': '5432',
    }
}
```
4. Update the broker and result backend settings in src/your_project/settings.py to use Redis:
```
CELERY_BROKER_URL = 'redis://redis:6379/0'
CELERY_RESULT_BACKEND = 'redis://redis:6379/0'
```
5. Start the application using Docker Compose:
```
docker-compose up
```
6. Access the CeleryTestApp in your web browser at http://localhost:8000.

## Usage
The CeleryTestApp allows you to perform the following tasks:

Scheduled tasks: Often there are tasks that need to be completed at a specific date and time: send a reminder to the user, end the trial period of the account, publish a post on social networks.

Send Email: Enter the recipient's email address, subject, and message in the input fields and click the "Send" button. The application will asynchronously send an email using Celery.

When performing these tasks, Celery handles them asynchronously in the background. The results of the calculations and email sending are stored in Redis, which serves as the backend for Celery. This allows the application to respond to other requests and perform other tasks without blocking the main execution thread.

You can track the progress and status of the tasks by viewing the logs in the terminal where the Celery worker is running. To start the Celery worker, run the following command:
```
docker-compose run --rm web celery -A your_project worker -l info
```
Tasks will be automatically processed by Celery, and the results will be returned to the application for display. This demonstrates the benefits of using asynchronous tasks and Celery to handle long-running operations or operations that can be executed in parallel without blocking the main application thread.

## Configuration
The Docker Compose setup includes the following services:

web: Django development server.
db: PostgreSQL database.
redis: Redis server.
celeryworker: Celery worker.
You can modify the configurations in the docker-compose.yml file according to your requirements.

## Contributing
Contributions are welcome! If you find any issues or have suggestions for improvements, please open an issue or submit a pull request on the GitHub repository.


 
