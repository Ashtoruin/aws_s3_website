# AWS Static Content Website

## Building
* build: `npm run-script build` (While in the frontend directory)
* run locally: `npm run-script start` (While in the frontend directory)

This requires nodejs installed to build and run locally. Changes to the content of the site can be made by editing the frontend/public/resumeData.json file.

## Deploying
This is deployed via github workflows `.github/workflows/main.yml` using cloudformation templates which reside in the `cft` folder. 

`bernau.io.yml` controls the bernau.io Route53 hostedzone which I've used for a custom DNS entry. Ideally the hostedzone CFT would live in it's own repo if this was for a production deployment but I decided to keep everything in one repo for this demo.

`main.yml` contains all the details relevant to this deployment. 

## Architecture
Since the main requirement was just a mechanism to deliver static content I decided to use S3 to host the content and front it with Cloudfront to speed up load times for end users and reduce the load on the S3 bucket itself. One downside of this however is updates to your website will potentially take longer to show up to end users. (Default is 24 hours though we could reduce this if required)

I used Route53 to give it a custom domain name and then ACM for a Certificate so we can also facilitate HTTPS traffic. 

If an API was required in the future for Dynamic content I would probably look at Lamdas behind an API Gateway or possibly a docker application behind a load balancer depending on what sort of load I was expecting.
