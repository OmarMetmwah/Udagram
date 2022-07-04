> # Hosting a Full-Stack Application Documentation

- The app is accessible via [this link](http://metmwah.s3-website-us-east-1.amazonaws.com/).

## Used Amazon Web Services


#### RDS Postgres
The application server uses AWS RDS Postgres as database for storing and retrieving information.

Database URI: `postgresql://postgres:password@database-1.cyahasayorxh.us-east-1.rds.amazonaws.com`

#### Elastic Beanstalk
The application server is deployed on AWS Elastic Beanstalk service. The application is build, archived and uploaded
to and S3 bucket from where Elastic Beanstalk extracts and runs the application on an endpoint.
  - I have added the environment variables in the production environment.
  - I have linked the database with the backend.
  - I have linked the backend with the frontend.

EB URL: `http://udagram-api-devv.eba-sj3uapcf.us-east-1.elasticbeanstalk.com`

#### S3 Bucket
The frontend application is deployed using AWS S3 Bucket. The bundled assets are uploaded to an S3 bucket and that
bucket is made publicly readable.

Bucket URL: `http://metmwah.s3-website-us-east-1.amazonaws.com/`

** End users can access the application from the Bucket URL. **


> ## Preparing Source Code Infrastructure For Deployment

- No environment variables that change from the development environment and production are present in the source code.

- A central configuration file is used in order to set the environment variables and make them available to the code and it lives [here](../udagram-api/src/config/config.ts).

- No authentication strings are hard-coded in the source code.

- A project-level package.json file contains All the necessary scripts for installing, building, testing, deploying both 
the frontend and the backend is added and it lives [here](../package.json).

- Screenshots of the AWS console indicate that RDS, EB and S3 are properly set up are available here [here](./AWS/).



> ## Configuring Continuous Integration Pipeline with Github
- I linked the Udagram project in github to circleci and added the `config.yml` file of the circleci containing all the orbs, jobs and workflows for running the pipeline automatically after every commit on the master branch.

- The `config.yml` file that ensures the build occurs in a logical sequence including Comments to explain the flow of the pipeline, is present [here](./Pipeline/config.yml).

- A screenshot of the last build shows that my CircleCi account is authorized to access my repo on Github and is detecting changes each time I am pushing to the master branch ![lives here](./Pipeline/circleci/Udagram-Pipeline-Build-Steps.png).

- All the secrets found in the application are configured inside CircleCi and passed to the production application. A screenshot of the configuration screen is present ![here](./Pipeline/circleci/Udagram-Environment-Variables.png) to show where secrets were added.

> ## Diagrams
- The submission contains a simple diagram giving a high-level:

 ![overview of the infrastructure](./AWS/Architecture-Diagram.png) 

and diagram showing the pipeline:

 ![overview of the pipeline](./Pipeline/circleci-Pipeline-Daigram.png). 

The diagram Includes the different AWS services used for hosting the DB, API and UI, A representation of the communication between the services is present in the diagrams.

> ## Pipeline Process Inside Circleci.
### Continuous integration:
- The scripts needed for installing, building, and deploying the frontend and backend of the application are found in the package.json files in `udagram-api & udagram-frontend` folders.
- The scripts are called in the project-level package.json.
- Jobs are added in the `.circleci/config.yml` file for running these scripts in the following order:-
  - install frontend
  - build frontend
  - install backend
  - build backend

### Continuous Deployment:
- The scripts needed for deploying the frontend and backend of the application are found in the package.json files in `udagram-api & udagram-frontend` folders.
- The scripts are called in the project-level package.json.
- Jobs are added in the `.circleci/config.yml` file for running these scripts in the following order:-
  - deploy frontend
  - deploy backend


