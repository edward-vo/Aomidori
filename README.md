# Aomidori
## 青緑「あおみどり」
Aomidori - A blue/green color

A blogging website built on AWS.

# Why Aomidori
Aomidori is an experement (at this time)

Curently, many websites exist where there are way more reads vs writes (think blog websites).

Websites like Wordpress store all data in a database. 

Aomidori instead S3 and Cloudfront to serve this content, then switches to a client-side router to give a CSR-like expereince.

# Reading Content
When a user reads a blog post (navigates to the route directly via a browser)
1. The user is served content directly from S3 via Cloudfront
2. The website loads a service-worker and switches to client-side routing
3. The website then loads a user micro-frontend, which checks for authentication and presents user options/authentication options
4. Instead of fetching HTML files, json (also static and served via S3) are sent to the user

When a user reads a blog post (website already loaded)
1. The site determins the type of page being visited.
2. The site re-renders the page template with the provided data

# Writing Content
When an admin wants to create a blog post
1. An admin create a post-request to the API of the site.
2. Cognito checks to ensure the user has the correct permissions
3. If the user does not have permissions to write, an error is thrown
4. The webite checks for the post bucket the user is writing to. Aomidori groups posts in buckets (see below)
5. Aomidory creates a JSON file which contains the current post, and previous post information (global and in bucket), then renders the HTML for the page
6. Aomidori re-visits the previous post content (both last post in bucket and globally JSON), adds the next post information, re-renders the previous post page (both last post in bucket and globally).
7. Aomidori invalides the Cloudfront cache for the relavent files

# Editing content
1. Cognito checks to ensure the user has the correct permissions
2. If the user does not have permissions to write, an error is thrown
3. Aomidori grabs the current content from the JSON
4. User POSTS new content
5. Permission check
6. Aomidori appends new content. Previous edits are stored by S3 (versioning)
7. Aomidori invalides the Cloudfront cache

# Comments and interactivity
Comments and upvotes/downvotes are handled client-side, as they are heavily dynamic.

## What is a post bucket
Many times blog posts may be related to certain other posts. This allows for better orginization.

For example, if someone is blogginging about the following:
- Travels
- Adventures of learning a 2nd language
- Clothing
- Book recomendations
- School
- etc.

If a user posts about travels, and then after clothing, then travels again, a reader who only wishes to see content about travels can navigate between posts without being interupted by the clothing posts.

Note: If the user wishes to view the very next post, they can still do so at this time


# Dependencies
I have not picked set dependencies. These are just ones that I will likely use

- TailwindCSS
- React
- Vite
- Typescript

# Cloud technologies
- S3
- Cloudfront
- Lambda
- API Gateway
- Route53
- Algolia Search (only non-aws tech, due to cost)
