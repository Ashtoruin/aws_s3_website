# AWS Static Content Website

## Building
* build: `npm run-script build` (While in the frontend directory)
* run locally: `npm run-script start` (While in the frontend directory)
This requires nodejs installed to build and run locally. Changes to the content of the site can be made by editing the frontend/public/resumeData.json file.

## Deploying
This is deployed via github workflows `.github/workflows/main.yml` using cloudformation templates which reside in the `cft` folder. `bernau.io.yml` controls the bernau.io Route53 hostedzone which I've used for a custom DNS entry. `main.yml` contains all the details relevant to this deployment. Ideally the hostedzone CFT would live in it's own repo if this was for a production deployment but I decided to keep everything in one repo for this demo.

## Architecture
Since the only requirement was delivering static content I decided to use S3 to host the content and front it with Cloudfront to speed up load times for end users and reduce the load on the S3 bucket itself if the bucket was to see enough load this would matter. I used Route53 to give it a custom domain name and then ACM for a Certificate so we can also facilitate HTTPS traffic also.