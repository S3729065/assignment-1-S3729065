# Simple Todo App with MongoDB, Express.js and Node.js
The ToDo app uses the following technologies and javascript libraries:
* MongoDB
* Express.js
* Node.js
* express-handlebars
* method-override
* connect-flash
* express-session
* mongoose
* bcryptjs
* passport
* docker & docker-compose

## What are the features?
You can register with your email address, and you can create ToDo items. You can list ToDos, edit and delete them. 

# How to use
First install the depdencies by running the following from the root directory:

```
npm install --prefix src/
```

To run this application locally you need to have an insatnce of MongoDB running. A docker-compose file has been provided in the root director that will run an insatnce of MongoDB in docker. TO start the MongoDB from the root direction run the following command:

```
docker-compose up -d
```

Then to start the application issue the following command from the root directory:
```
npm run start --prefix src/
```

The application can then be accessed through the browser of your choise on the following:

```
localhost:5000
```

## Testing

Basic testing has been included as part of this application. This includes unit testing (Models Only), Integration Testing & E2E Testing.

### Linting:
Basic Linting is performed across the code base. To run linting, execute the following commands from the root directory:

```
npm run test-lint --prefix src/
```

### Unit Testing
Unit Tetsing is performed on the models for each object stored in MongoDB, they will vdaliate the model and ensure that required data is entered. To execute unit testing execute the following commands from the root directory:

```
npm run test-unit --prefix src/
```

### Integration Testing
Integration testing is included to ensure the applicaiton can talk to the MongoDB Backend and create a user, redirect to the correct page, login as a user and register a new task. 

Note: MongoDB needs to be running locally for testing to work (This can be done by spinning up the mongodb docker container).

To perform integration testing execute the following commands from the root directory:

```
npm run test-integration --prefix src/
```

### E2E Tests
E2E Tests are included to ensure that the website operates as it should from the users perspective. E2E Tests are executed in docker containers. To run E2E Tests execute the following commands:

```
chmod +x scripts/e2e-ci.sh
./scripts/e2e-ci.sh
```


###### This project is licensed under the MIT Open Source License

# Documentation: Simple TODO App - Daniel (S3729065)

## The Problem:
Writing a _"config.yml"_ in the hidden directory of _".cirlceci"_ first requires me to write code in a top-down approach.
The first problem is as to how do I write the code in a way that incorporates Docker as an image when executed and running in a CircleCI continuous integration environment.

Our first problem is as to how to ensure that the Node Package Manager (NPM) can actually find the desired files and directories, since everytime we run a job, it creates a new kind of instance, in which it treats jobs like components - this somewhat akin to how stub or mock tests work but in an automated manner.

The second problem consists of ensuring runtime is lower than 10 to 15 minutes. So a top-down approach where, the fastest jobs are first-in and first-out (FIFO).

Third problem is as to how do we ensure that the codes actually work without any additional bash command execution?
A "chmod" for file permissions is already available in the E2E Tests' solution (in this same README.md). But I have across NPM errors where I get an exit code of 34. - **The solution** to this being the inclusion of _"- checkout"_ and below it the same command created as a CircleCI's config.yml "commands" code: _"- install_deps"_

## The Solutions

Following the ToDo App solutions for using the already given technologies and javascript libraries. The solutions were just coming at the problems in a top-down approach.

### Jobs:
First I ensured that I have the _" --prefix src/"_ was at the end of each NPM run command, because without it, it could not find the files or directories.

All the jobs would have the _"- checkout"_ and the _"- install_dependencies"_ codes as the first two lines in their steps, this makes sure the scripts actually find the Node modules and necessary files to run.

### Workflows:
My Workflows, in a top-down approach first ensures that the Build and Pack jobs (noted as _"- build"_ and _"- pack"_ in the _workflows_ code, near the bottom) ... ensures that these jobs succeed first before the other jobs run, since both Build and Pack jobs have a faster compilation time than the other jobs.

### Build and Pack
Build and Pack both utilise the _"- checkout"_ and the _"- install_dependencies"_ codes.
These make sure that the Docker image actually installs the necessary Node modules so that it'll not fail with a file or directory permission error or a non-existing error. This error occurs as an NPM exiting error codes: 34 (file permissions error) and 254 (file or directory non-existing error).

The Build job has the Docker username and password as environment vairables configured through the CircleCI web-app, thus providing additional security for my Docker authentication.

The Pack job, stores the artifacts in a TGZ compressed file as: simpletodoapp-1.0.0.tgz

### Jest-JUnit: Unit Test
Again, _"- checkout"_ and the _"- install_dependencies"_ codes are used to make Jest-JUnit pass. The same problem also occurred with the NPM exit code: 254, and was solved with the _"- checkout"_ and the _"- install_dependencies"_ codes.

Jest-JUnit's environment is: "JEST_JUNIT_OUTPUT_DIR: test/unit" following the "package.json" file's contents and the project's file heirarchy.

_"npm run test-unit --prefix src/"_ is run in the "jest" job. This passed.

### Linting

Linting is similar to the other jobs, and its only running command is:
_"- run: name: Linting command: | npm run test-lint --prefix src/"_

### Code Coverage

Employing a bash and curl, the run command is simply:
_"- run: name: Validate Code Coverage command: | bash <(curl -s https://codecov.io/bash)"_ as taught in the tutorial and lectorial.

### Scan Secure: Node JS Scan

The commands for this one was the installation for the NodeJS Scan module and the Node JS Scan's own command to do a parse report.

