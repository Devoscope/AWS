# AWS CloudFront Notes

## What is AWS CloudFront?
AWS CloudFront is a content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds.

## Key Features
- **Global Content Delivery**: Uses a network of edge locations to cache and distribute content closer to users.
- **Security**: Integrates with AWS Shield, AWS WAF, and supports HTTPS.
- **Performance Optimization**: Supports Gzip & Brotli compression and HTTP/2 for faster loading.
- **Customization**: Allows Lambda@Edge for real-time request and response modifications.
- **Origin Support**: Works with AWS S3, EC2, ELB, and custom origins.
- **Caching**: Configurable TTL settings to optimize cache hit ratio.

## How CloudFront Works
1. A user requests content via a URL.
2. CloudFront checks its edge locations for a cached copy.
3. If cached, it serves the content; otherwise, it fetches it from the origin.
4. The response is cached at the edge for future requests.

## Pricing Model
- **Data Transfer Out**: Charges based on region and outbound data.
- **Requests**: Billed per HTTP/HTTPS request.
- **Invalidation Requests**: First 1,000 per month are free.
- **Origin Fetches**: Charged when fetching data from the origin.

## CloudFront Key Components
- **Distribution**: A CloudFront setup that consists of an origin, cache behavior, and settings.
- **Origin**: The source server where CloudFront fetches the content.
- **Edge Locations**: Data centers where cached content is stored.
- **Behaviors**: Rules to control caching, compression, and access.

## Common Use Cases
- Website acceleration
- Video streaming
- API acceleration
- Security & DDoS protection

## Setting Up CloudFront
1. **Create a CloudFront Distribution**
2. **Specify Origin (S3, EC2, etc.)**
3. **Configure Cache Behaviors**
4. **Enable SSL/HTTPS**
5. **Deploy and Test**

## CloudFront with AWS S3
- Enable **static website hosting** on S3.
- Configure the bucket policy to allow public access or use OAI (Origin Access Identity) for secure access.
- Use CloudFront to serve S3 content with enhanced performance.

## Monitoring & Logging
- AWS CloudWatch for metrics.
- AWS CloudTrail for request logging.
- Access logs stored in S3.

## Invalidating Cache
Use `Invalidations` to remove outdated content:
```sh
aws cloudfront create-invalidation --distribution-id <DISTRIBUTION_ID> --paths "/*"
```

## Security Best Practices
- Use **Origin Access Control (OAC)** for private S3 access.
- Enable **HTTPS** and restrict HTTP.
- Use **AWS WAF** for additional protection.

## Alternatives to AWS CloudFront
- Akamai CDN
- Fastly
- Cloudflare CDN
- Google Cloud CDN
- Azure Front Door
