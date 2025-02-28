---
title: Basic Concepts
parent: CI/CD
nav_order: 71
layout: default
---

## Basic Concepts of CI/CD

CI/CD, standing for Continuous Integration, Continuous Delivery, and Continuous Deployment, is a set of practices designed to enable faster and more reliable software releases. It automates the steps involved in building, testing, and deploying code changes.

---

### Continuous Integration (CI)

- **Definition:** CI is the practice of frequently merging code changes from all developers into a central repository, followed by automated builds and tests. The primary goal of CI is to detect integration problems early and often.
- **Key Practices:**
  - **Version Control:** All code is managed in a version control system (like Git).
  - **Frequent Commits:** Developers commit their code changes multiple times a day to the main branch (or feature branches that are regularly merged).
  - **Automated Builds:** Every commit triggers an automated build process. This typically includes compiling the code (if necessary), running linters, and performing other code quality checks.
  - **Automated Testing:** A comprehensive suite of automated tests (unit tests, integration tests, etc.) is run as part of the build process.
  - **Fast Feedback:** Developers receive rapid feedback (usually within minutes) on whether their changes broke the build or any tests.
- **Benefits:**
  - **Early Bug Detection:** Integration issues and bugs are found much earlier in the development cycle, making them easier and cheaper to fix.
  - **Reduced Integration Problems:** Frequent integration minimizes the risk of large, complex, and difficult-to-resolve merge conflicts.
  - **Improved Code Quality:** Automated testing and code analysis enforce coding standards and best practices.
  - **Faster Release Cycles:** CI enables faster and more frequent releases by automating much of the build and testing process.
- **Example Workflow:**
  1. Developer commits code changes to a shared Git repository.
  2. A CI server (like Jenkins, GitLab CI, CircleCI, GitHub Actions) detects the commit.
  3. The CI server checks out the code, builds the application, and runs automated tests.
  4. If the build or any tests fail, the developers are notified immediately.
  5. If the build and tests pass, the code is ready for the next stage (delivery/deployment).

---

### Continuous Delivery (CD)

- **Definition:** CD is an extension of CI. It focuses on automating the software release process _after_ the CI stage. With CD, every code change that passes the CI stage is _ready_ to be deployed to production, but the actual deployment is typically triggered _manually_.
- **Key Practices:**
  - **Everything from CI:** Builds upon all the practices of CI.
  - **Automated Release Process:** The steps required to release the software (e.g., packaging, creating releases, deploying to staging environments) are automated.
  - **Release Artifacts:** The CI process produces deployable artifacts (e.g., Docker images, executable files, packages).
  - **Staging Environments:** Changes are typically deployed to one or more staging environments (that mirror production) for final testing and validation.
  - **Manual Approval (usually):** Deployment to production usually requires manual approval, although this can be automated in some cases.
- **Benefits:**
  - **Reduced Risk:** Releases are smaller and more frequent, reducing the risk of deploying faulty code.
  - **Faster Time to Market:** New features and bug fixes can be released to users much faster.
  - **Repeatable and Reliable Releases:** The automated release process ensures consistency and reduces the chance of human error.
  - **Increased Confidence:** Thorough automated testing at every stage increases the confidence to deploy frequently.

---

### Continuous Deployment (CD)

- **Definition:** Continuous Deployment is the most advanced stage, fully automating the entire process. Every code change that passes all stages of the CI/CD pipeline is _automatically_ deployed to production _without any manual intervention_.
- **Key Practices:**
  - **Everything from Continuous Delivery**: Builds upon all the practices of CI and CD.
  - **Fully Automated Deployments:** No manual approvals are required. Successful builds and tests automatically trigger deployments to production.
  - **Advanced Monitoring:** Robust monitoring and alerting systems are crucial to detect and respond to any issues that arise in production.
  - **Automated Rollbacks:** The ability to automatically roll back to a previous version if problems are detected after deployment.
  - **Feature Flags/Toggles:** Often used to control the release of new features to users, allowing for gradual rollouts and A/B testing.
- **Benefits:**
  - **Extremely Fast Release Cycles:** New features and bug fixes are delivered to users as quickly as possible.
  - **Continuous Feedback:** User feedback on new changes is obtained almost immediately.
  - **Maximum Efficiency:** The entire software release process is fully automated, freeing up developers to focus on writing code.
- **Requirements**: Continuous Deployment requires a very high level of confidence in the automated testing and deployment process. It's not suitable for all organizations or all projects.

---

### Key Terminology

- **Pipeline:** A series of automated steps that take code changes from version control through build, test, and deployment.
- **Build:** The process of compiling code, running linters, and preparing the software for testing.
- **Artifact:** The output of the build process (e.g., a Docker image, a .jar file, a .zip file).
- **Unit Test:** Tests individual components or modules of the code in isolation.
- **Integration Test:** Tests the interaction between different components or modules.
- **End-to-End (E2E) Test:** Tests the entire application flow from start to finish, often simulating user interactions.
- **Staging Environment:** An environment that closely mirrors the production environment, used for final testing before deployment.
- **Production Environment:** The live environment where the application is accessible to users.
- **Rollback:** Reverting to a previous version of the application, usually due to a failed deployment or a critical bug.
- **CI/CD Server (or Orchestrator):** A tool that automates the CI/CD pipeline (e.g., Jenkins, GitLab CI, CircleCI, GitHub Actions, Travis CI, Bamboo).
- **Feature Flag/Toggle:** A mechanism to enable or disable features in production without deploying new code. This is useful for testing new features with a subset of users or for quickly disabling a feature if it causes problems.

---
