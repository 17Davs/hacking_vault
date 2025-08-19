Quick Testing Workflow for HTTP Request Smuggling

[[3. Finding HTTP Request Smuggling]]

1. **Initial Recon**
    - Look for endpoints that accept **POST requests**.    
    - Check if both `Content-Length` and `Transfer-Encoding` headers are allowed.
        
2. **Step 1 – Timing Tests**
    - Send **CL.TE timing payload** first.
    - If no delay → try **TE.CL timing payload**.
    - Watch for **delayed responses** (server “waiting” = possible vulnerability).
        
3. **Step 2 – Confirm with Differential Responses**
    - Craft **attack request** (depends on CL.TE vs TE.CL).
    - Immediately send **normal request** on a separate connection.
    - If the normal request is corrupted → vulnerability confirmed.
    
4. **Step 3 – Double-Check Consistency**
    - Ensure both attack & normal requests use the **same URL and parameters** (max chance of hitting same back-end).
    - Repeat multiple times if the site is busy or uses load balancing.
        
5. **Safety Notes** ⚠️
    - Do NOT test blindly on production → can corrupt real user requests.
    - Always test **CL.TE first** (less disruptive).
    - Use lab environments (e.g., PortSwigger Academy) for practice.
