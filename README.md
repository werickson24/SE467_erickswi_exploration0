This is a simple Single Page [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.


This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Deploy on AWS S3

To deploy this application as a static website on AWS S3, follow these steps:

1. Build the static site:
```bash
npm run build
```

2. The static files will be generated in the `out` directory.

3. Create an S3 bucket in AWS:
   - Go to AWS S3 Console
   - Create a new bucket with a unique name
   - Enable "Static website hosting" in the bucket properties
   - Set the index document to "index.html"
   - Set the error document to "404.html"

4. Configure bucket permissions:
   - Add a bucket policy to make the contents public:
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
        }
    ]
}
```

5. Upload the contents of the `out` directory to your S3 bucket:
```bash
aws s3 sync out/ s3://YOUR-BUCKET-NAME
```

Your site will be available at the S3 bucket's website endpoint: `http://YOUR-BUCKET-NAME.s3-website-REGION.amazonaws.com`

