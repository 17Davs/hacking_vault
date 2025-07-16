  
Here is a short breakdown of the in-built browser tools you will use throughout this room:
- **View Source** - Use your browser to view the human-readable source code of a website.
- **Inspector** - Learn how to inspect page elements and make changes to view usually blocked content.
- **Debugger** - Inspect and control the flow of a page's JavaScript
- **Network** - See all the network requests a page makes.
## Viewing Page Source

- Comments can be dangerous and may reveal sensitive information.
- Look out for extra links that might expose hidden or unintended resources.
- Watch for directory listings (e.g., CSS, JavaScript, or images) that could lead to sensitive files.
- Search for framework information, which might leak version details and aid in identification.

## Developer Tools - Inspector

- Use the Inspector to locate and modify page elements (e.g., DIV with class premium-customer-blocker) to reveal hidden content.
- Change CSS styles, such as switching display: block to display: none, to uncover blocked areas or flags.
- Add new styles or edit content temporarily to test visibility—changes are local and reset on refresh.
- Experiment with element editing to understand how websites render, but note it’s only for your browser session.

## Developer Tools - Debugger

- Use the Debugger (or Sources in Chrome) to inspect and control JavaScript flow on a webpage.
- Explore resource lists to find JavaScript files (e.g., flash.min.js) that might contain interesting code.
- Apply "Pretty Print" to minified or obfuscated JavaScript to improve readability, though obfuscation can still obscure intent.
- Look for unusual code behaviors (e.g., rapid flashes) that might hide security-relevant actions or data.

## Developer Tools - Network

- Use the Network tab to monitor all external requests a webpage makes.
- Refresh the page to capture a full list of requested files, helping identify potential vulnerabilities.
- Check for unexpected or sensitive resource requests that could leak information.
- Example: Spotting an unusual .php file request might indicate a backend script worth investigating.