# The Discovery Center School Website

A modern, responsive website for The Discovery Center School in San Francisco, CA. This website showcases the school's mission, values, curriculum, and admissions information in a contemporary design.

## Features

- **Modern Design**: Clean, professional layout with smooth animations
- **Fully Responsive**: Works seamlessly on desktop, tablet, and mobile devices
- **Fast Performance**: Optimized CSS and JavaScript for quick load times
- **SEO Friendly**: Semantic HTML and proper meta tags
- **Accessible**: WCAG compliant with proper ARIA labels
- **Interactive**: Smooth scrolling, animated sections, and form validation
- **Secure**: Security headers configured for Cloudflare Pages

## Project Structure

```
Webpage_agentic_system/
├── index.html          # Main HTML file
├── styles.css          # All styling
├── script.js           # Interactive JavaScript
├── _headers            # Cloudflare security headers
├── robots.txt          # SEO configuration
├── package.json        # Node.js configuration
├── .gitignore         # Git ignore rules
└── README.md          # This file
```

## Local Development

### Option 1: Using Python (Recommended for quick testing)

```bash
# Navigate to the project directory
cd /Users/hydrogeo/Downloads/Webpage_agentic_system

# Start a local server
python3 -m http.server 8000

# Or using Python 2
python -m SimpleHTTPServer 8000
```

Then open your browser to `http://localhost:8000`

### Option 2: Using Node.js

```bash
# Install http-server globally
npm install -g http-server

# Run the server
http-server -p 8000
```

### Option 3: Using VS Code Live Server

1. Install the "Live Server" extension in VS Code
2. Right-click on `index.html`
3. Select "Open with Live Server"

## Deploying to Cloudflare Pages

### Method 1: Using Cloudflare Dashboard (Recommended for beginners)

1. **Prepare Your Code**
   ```bash
   cd /Users/hydrogeo/Downloads/Webpage_agentic_system
   git add .
   git commit -m "Modern DCS website ready for deployment"
   ```

2. **Push to GitHub**
   ```bash
   # Create a new repository on GitHub first, then:
   git remote add origin https://github.com/YOUR_USERNAME/dcs-website.git
   git branch -M main
   git push -u origin main
   ```

3. **Connect to Cloudflare Pages**
   - Go to [Cloudflare Dashboard](https://dash.cloudflare.com/)
   - Navigate to "Workers & Pages" > "Pages"
   - Click "Create application" > "Connect to Git"
   - Authorize GitHub and select your repository
   - Configure build settings:
     - **Build command**: Leave empty (static site)
     - **Build output directory**: `/`
     - **Root directory**: `/`
   - Click "Save and Deploy"

4. **Custom Domain (Optional)**
   - In your Cloudflare Pages project, go to "Custom domains"
   - Click "Set up a custom domain"
   - Enter `www.dcssf.com` (or your domain)
   - Follow DNS configuration instructions

### Method 2: Using Wrangler CLI (Advanced)

1. **Install Wrangler**
   ```bash
   npm install -g wrangler
   # or
   npm install
   ```

2. **Login to Cloudflare**
   ```bash
   wrangler login
   ```

3. **Deploy**
   ```bash
   # Deploy to production
   wrangler pages deploy . --project-name=dcs-website

   # Or use the npm script
   npm run deploy
   ```

4. **Set Custom Domain**
   ```bash
   wrangler pages domains add www.dcssf.com --project-name=dcs-website
   ```

### Method 3: Direct Upload

1. Go to [Cloudflare Pages](https://pages.cloudflare.com/)
2. Click "Create a project"
3. Choose "Direct Upload"
4. Drag and drop all files (or select them)
5. Click "Deploy site"

## Configuration

### Security Headers

The `_headers` file includes:
- X-Frame-Options (prevents clickjacking)
- Content-Security-Policy
- X-Content-Type-Options
- Referrer-Policy
- Proper cache control for assets

### Environment Variables (Optional)

If you need to add environment variables:

1. In Cloudflare Pages Dashboard:
   - Go to your project settings
   - Click "Environment variables"
   - Add your variables

2. Common variables you might need:
   ```
   CONTACT_EMAIL=admissions@dcssf.com
   GOOGLE_ANALYTICS_ID=UA-XXXXXXXXX-X
   ```

## Customization Guide

### Updating Content

1. **Text Content**: Edit `index.html` directly
2. **Colors**: Modify CSS variables in `styles.css` (`:root` section)
3. **Contact Information**: Update in `index.html` contact section
4. **Navigation**: Add/remove links in the `<nav>` section

### Adding Real Images

Replace the SVG placeholders with actual images:

```html
<!-- Replace this -->
<div class="image-placeholder">
  <svg>...</svg>
</div>

<!-- With this -->
<img src="path/to/your/image.jpg" alt="Description" loading="lazy">
```

### Color Scheme

Current colors are defined in `styles.css`:

```css
:root {
    --primary-color: #1E3A8A;    /* Deep Blue */
    --secondary-color: #F59E0B;  /* Amber */
    /* Modify these to match your brand */
}
```

## Adding Features

### Google Analytics

Add before closing `</head>` tag in `index.html`:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

### Contact Form Backend

To make the contact form functional, you have several options:

#### Option 1: Cloudflare Workers (Recommended)

Create a Worker to handle form submissions:

```javascript
// worker.js
export default {
  async fetch(request) {
    if (request.method === 'POST') {
      const formData = await request.json();

      // Send email via Cloudflare Email Workers
      // or integrate with SendGrid, Mailgun, etc.

      return new Response(JSON.stringify({ success: true }), {
        headers: { 'Content-Type': 'application/json' }
      });
    }
    return new Response('Method not allowed', { status: 405 });
  }
};
```

#### Option 2: Third-Party Form Services

- [Formspree](https://formspree.io/)
- [Netlify Forms](https://www.netlify.com/products/forms/)
- [Web3Forms](https://web3forms.com/)

Update the form in `index.html`:

```html
<form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
  <!-- form fields -->
</form>
```

## Performance Optimization

The website is already optimized with:
- Minified CSS
- Efficient JavaScript
- Lazy loading ready
- Proper caching headers
- CSS containment
- Reduced animations on mobile

### Further Optimizations

1. **Image Optimization**
   - Use WebP format
   - Compress images with tools like TinyPNG
   - Use responsive images with `srcset`

2. **Font Optimization**
   - Currently using Google Fonts with preconnect
   - Consider self-hosting fonts for even better performance

3. **JavaScript Optimization**
   - Already using modern vanilla JS (no frameworks)
   - Consider adding a build step with Vite or Parcel if needed

## Browser Support

- Chrome/Edge (latest 2 versions)
- Firefox (latest 2 versions)
- Safari (latest 2 versions)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Troubleshooting

### Deployment Issues

**Problem**: 404 error after deployment
- **Solution**: Ensure `index.html` is in the root directory

**Problem**: CSS/JS not loading
- **Solution**: Check file paths are relative, not absolute

**Problem**: Custom domain not working
- **Solution**: Verify DNS records in Cloudflare Dashboard

### Local Development Issues

**Problem**: Port already in use
- **Solution**: Use a different port: `python3 -m http.server 8001`

**Problem**: CORS errors
- **Solution**: Always use a local server, don't open HTML files directly

## Support and Contact

For issues with this website:
- Email: admissions@dcssf.com
- Phone: (415) 724-7458
- Address: 1442 Fulton St, San Francisco, CA 94117

## License

This website is proprietary to The Discovery Center School.

## Credits

- Design & Development: Refactored for modern web standards
- Original Content: The Discovery Center School
- Fonts: Google Fonts (Inter, Playfair Display)
- Hosting: Cloudflare Pages

## Changelog

### Version 1.0.0 (2024)
- Initial modern refactor
- Responsive design implementation
- Cloudflare Pages optimization
- Interactive features and animations
- Contact form integration ready
- SEO and accessibility improvements

---

**Need help?** Check the [Cloudflare Pages documentation](https://developers.cloudflare.com/pages/) or contact your web developer.
