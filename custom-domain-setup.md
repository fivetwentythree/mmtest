# Setting Up a Custom Domain for Your GitHub Pages Site

## Overview
This guide will walk you through the process of setting up a custom domain for your GitHub Pages site. By following these steps, you'll be able to serve your site from your own domain name instead of the default `username.github.io` domain.

## Prerequisites
- A registered domain name from a domain registrar (like GoDaddy, Namecheap, Google Domains, etc.)
- Access to your domain's DNS settings
- Your GitHub Pages site is already set up and running

## Steps

### 1. Configure DNS Settings

#### For an apex domain (example.com):
Add these A records in your domain registrar's DNS settings:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

#### For a subdomain (www.example.com):
Add a CNAME record:
- Type: CNAME
- Host: www
- Value: `<username>.github.io`

### 2. Configure GitHub Pages Settings

1. Go to your repository settings
2. Navigate to "Pages" section
3. Under "Custom domain", enter your domain name
4. Click "Save"
5. Check "Enforce HTTPS" (available after DNS propagation)

### 3. Add CNAME File

GitHub will automatically create a CNAME file in your repository, but if you want to maintain it manually:

1. Create a file named `CNAME` in your repository's root directory
2. Add your custom domain to the file (e.g., `www.example.com`)
3. Commit and push the changes

### 4. Wait for DNS Propagation

- DNS changes can take up to 24-48 hours to propagate globally
- You can check propagation status using tools like [whatsmydns.net](https://whatsmydns.net)

### 5. Verify Setup

1. Check if your site is accessible via your custom domain
2. Verify that HTTPS is working correctly
3. Test both www and non-www versions of your domain

## Troubleshooting

### Common Issues

1. **404 Errors**
   - Verify your DNS settings
   - Check if the CNAME file exists and contains the correct domain

2. **SSL Certificate Issues**
   - Wait for DNS propagation
   - Ensure "Enforce HTTPS" is enabled in GitHub Pages settings

3. **Domain Not Resolving**
   - Double-check A records or CNAME configuration
   - Clear your local DNS cache
   - Wait for DNS propagation

### DNS Verification

Use these commands to verify your DNS configuration:

```bash
# For A records
dig +noall +answer example.com

# For CNAME
dig +noall +answer www.example.com
```

## Best Practices

1. Always use HTTPS
2. Regularly monitor your SSL certificate
3. Keep your DNS records clean and documented
4. Consider using a DNS provider with good documentation and support

## Additional Resources

- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Managing a Custom Domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [Troubleshooting Custom Domains](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages)

## Support

If you encounter issues:
1. Check GitHub Status Page
2. Review GitHub Pages documentation
3. Search GitHub Community forums
4. Contact your domain registrar's support for DNS-related issues


## Migrating from Subdomain to Root Domain

### Overview
If you're currently hosting your site on a subdomain (e.g., `blog.example.com`) and want to move it to a root domain (e.g., `example.com`), follow these additional steps:

### 1. Update DNS Configuration

1. Remove existing CNAME record for your subdomain
2. Add these A records for your root domain:
   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```
3. Optionally, add a www CNAME record pointing to your root domain

### 2. Update GitHub Repository Settings

1. Go to your repository settings
2. In the "Pages" section, update your custom domain to the root domain
3. Wait for GitHub to verify your new DNS settings
4. Ensure HTTPS is still enforced

### 3. Update CNAME File

1. Edit the CNAME file in your repository
2. Replace the subdomain with your root domain
3. Commit and push the changes

### 4. Additional Considerations

1. **SEO Impact**
   - Set up 301 redirects from old subdomain to new domain
   - Update any hardcoded links in your content
   - Update search console properties

2. **DNS Propagation**
   - Allow 24-48 hours for full propagation
   - Monitor both old and new domains during transition

3. **SSL Certificates**
   - GitHub will automatically provision a new certificate
   - Wait for the certificate to be issued before enforcing HTTPS