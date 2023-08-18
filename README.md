# AWS-Blogger
An experement with CSR &amp; Prerendering/SSR

# AWS Archetecture
This uses the following servies:
- OpenSearch (Opt)
- CloudFront
- S3
- AWS Lambda
- AWS Cognito
- API Gateway

When a user creates a blog post, the lambda is triggered. This causes 2 files to be created:
- (PostGroup)/(BlogPostSlug).html
- (PostGroup)/(BlogPostSlug).json

The first html pre-rendered via a lambda function. After the page is loaded, the client-side router takes over and content is then rendered on the client (fetching data via the json files instead).

This POC is an experement with creating a blogging website with the performance of a static site but with the fun features of a client-side rendered application.

# Dependencies
I have not picked set dependencies. These are just ones that I will likely use

- TailwindCSS
- React
- Vite
- Typescript
