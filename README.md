# Chrome Security Bypass Tool

## Overview
This project implements a browser-based tool that leverages Chrome's security architecture to bypass content filtering systems like Securly on Chrome-enabled devices. The application works by exploiting Chrome's security model, where local HTML files have privileged access that cannot be intercepted by extension-based monitoring systems.

## How It Works
When launched, the HTML file presents a user interface requesting the target URL. The application then loads the requested content within a protected context that filtering extensions cannot monitor or block due to Chrome's built-in privacy boundaries between local files and extensions.

### Technical Implementation Details
The tool uses a simple yet effective approach:

1. **Local HTML Execution**: When an HTML file is opened locally (as a `file://` protocol), Chrome grants it special privileges that extension-based monitoring systems cannot access.

2. **iframe Implementation**: The core functionality uses an iframe element to load external web content. The iframe is styled to take up the full viewport:
   ```javascript
   const i = document.getElementById('i');
   const a = i.style;
   a.border = a.outline = 'none';
   a.width = '100%';
   a.height = '100%';
   a.position = 'fixed';
   a.left = a.right = a.top = a.bottom = '0';
   ```

3. **URL Handling**: The script prompts the user for a URL and then loads it within the iframe:
   ```javascript
   let k = prompt('Enter a URL:');
   s(k);
   ```

4. **HTTP Protocol Enforcement**: The tool automatically prepends "http://" to ensure proper loading:
   ```javascript
   i.src = `http://${v}`;
   ```

5. **Minimal Footprint**: The HTML uses a tiny transparent favicon encoded in base64 to minimize detectability.

6. **Security Mechanism**: This approach works because Chrome's security model prevents extensions from modifying or monitoring content inside local files, creating a bypass channel for content filtering.

## Current Limitations
- The application is currently in early development stages
- Some websites may display incorrectly or with limited functionality
- Performance issues may occur with complex web applications
- Occasional instability or navigation problems may be encountered
- HTTPS sites may require manual protocol adjustment
- Certain web applications with strict security policies may not function properly in the iframe

## Installation & Usage
1. Download the HTML file
2. Open the file in Chrome
3. When prompted, enter the URL you wish to access (without http:// as it's added automatically)
4. The requested website will load in fullscreen mode within your browser

## Technical Details
The tool utilizes Chrome's same-origin policy and security sandbox to create a protective layer between content filtering extensions and requested web content. This approach is fundamentally different from traditional proxy-based solutions.

Extension-based filtering systems like Securly operate by monitoring and intercepting network requests within the browser. However, Chrome's security model prevents extensions from accessing content within local files to protect user privacy. This tool leverages that protection as a feature to bypass the filtering mechanisms.

## Legal Notice
This tool is provided for educational purposes only. Users should ensure compliance with their organization's acceptable use policies and relevant laws before implementation.

---

*This README has been rewritten by Claude to be more understandable and professional.*
