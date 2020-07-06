[ HOME ](README.md)
# Read 42 - Deployment, ElephantSQL and Docker on Heroku

# Deployment

The easiest way to deploy Next.js to production is to use the Vercel platform from the creators of Next.js. Vercel is an all-in-one platform with Global CDN supporting static & JAMstack deployment and Serverless Functions.

1. Sign up to Vercel (no credit card is required).
1. After signing up, you’ll arrive on the “Import Project” page. Under “From Git Repository”, choose the Git provider you use and set up an integration. (Instructions: GitHub / GitLab / BitBucket).
1. Once that’s set up, click “Import Project From …” and import your Next.js app. It auto-detects that your app is using Next.js and sets up the build configuration for you. No need to change anything — everything should work just fine!
1. After importing, it’ll deploy your Next.js app and provide you with a deployment URL. Click “Visit” to see your app in production.
1. Congratulations! You’ve just deployed your Next.js app! If you have questions, take a look at the Vercel documentation.

### DPS: Develop, Preview, Ship

- Develop: Write code in Next.js. Keep the development server running and take advantage of React Fast Refresh.
- Preview: Every time you push changes to a branch on GitHub / GitLab / BitBucket, Vercel automatically creates a new deployment with a unique URL. You can view them on GitHub when you open a pull request, or under “Preview Deployments” on your project page on Vercel. Learn more about it here.
- Ship: When you’re ready to ship, merge the pull request to your default branch (e.g. master). Vercel will automatically create a production deployment.

### Custom Domains, Environment Variables, Automatic HTTPS, and more
- Custom Domains: Once deployed on Vercel, you can assign a custom domain to your Next.js app. Take a look at our documentation here.
- Environment Variables: You can also set environment variables on Vercel. Take a look at our documentation here. You can then use those environment variables in your Next.js app.
- Automatic HTTPS: HTTPS is enabled by default (including custom domains) and doesn't require extra configuration. We auto-renew SSL certificates.

----------
# ElephantSQL

> ElephantSQL is a PostgreSQL database hosting service. ElephantSQL will manage administrative tasks of PostgreSQL, such as installation, upgrades to latest stable version and backup handling.

ElephantSQL is also integrated to several cloud application platforms (also known as PaaS). With a click of a button your database is provisioned in the same data center as your application is hosted, and is ready to be used immediately.

- ElephantSQL automates every part of setup and running of PostgreSQL clusters. Available on all major cloud and application platforms all over the world. Let your team focus on what they do best - building your product. Leave server management and monitoring to the experts.
- lephantSQL is hosted by PostgreSQL experts, with several years of DBA PostgreSQL experience. We provide 24/7 support to thousands of customers.
- Automated backups are performed every day, which is stored in a cloud file storage so that they are always accessible to you. You can also use point-in-time-recovery to restore your database.


_______
# Docker on Heroku

Create a heroku.yml file in your application’s root directory. The following example heroku.yml specifies the Docker image to build for the app’s web process:
```
build:
  docker:
    web: Dockerfile
run:
  web: bundle exec puma -C config/puma.rb
```
In this example, both heroku.yml and Dockerfile are in the same directory. If the Dockerfile lives in a non-root directory, specify the relative path in the build.docker.web value, such as app/Dockerfile.

If you don’t include a run section, Heroku uses the CMD specified in the Dockerfile.

Commit the file to your repo:
```
git add heroku.yml
git commit -m "Add heroku.yml"
Set the stack of your app to container:
```
heroku stack:set container
```
Push your app to Heroku:

git push heroku master
```
Your application will be built, and Heroku will use the run command provided in heroku.yml instead of your Procfile.


### Heroku.yml manifest has 4 top-level sections:

1. **setup** - Specifies the add-ons and config vars to create during app provisioning
1. **build** - Specifies the Dockerfile to build
1. **release** - Specifies the release phase tasks to execute
1. **run** - Specifies process types and the commands to run for each

```
setup:
  addons:
    - plan: heroku-postgresql
      as: DATABASE
  config:
    S3_BUCKET: my-example-bucket
build:
  docker:
    web: Dockerfile
    worker: worker/Dockerfile
  config:
    RAILS_ENV: development
    FOO: bar
release:
  command:
    - ./deployment-tasks.sh
  image: worker
run:
  web: bundle exec puma -C config/puma.rb
  worker: python myworker.py
  asset-syncer:
    command:
      - python asset-syncer.py
    image: worker
```

### Known issues and limitations

- Although Review Apps are currently supported, pipeline promotions are not.
- Private Spaces do not honor the run section in heroku.yml yet, so the command must instead be specified via the Dockerfile.
- The Docker build context is always set to the directory containing the Dockerfile and cannot be configured independently.
- While Docker images are not subject to size restrictions (unlike slugs), they are subject to the dyno boot time restriction. As layer count/image size grows, so will dyno boot time. See the best practices for writing Dockerfiles guide for suggestions on how to reduce Docker image size.
- Images with more than 40 layers may fail to start in the Common Runtime.
- The Dockerfile commands listed here are not supported.

# Sources
[Deployment](https://nextjs.org/docs/deployment)

[elephantsql](https://www.elephantsql.com/)

[Docker on Heroku](https://devcenter.heroku.com/articles/build-docker-images-heroku-yml)
