How to redirect CloudFlare's domain name to Sedo's domain name sales address (or any address)?

As a domain investor, you want your domain to be noticed by potential buyers. Buyers may test the domain by directly typing it into their browser. In this case, redirecting to a sales link on Sedo or another domain marketplace is a great solution.

### Step 1: Create Three DNS A Records

Click `CloudFlare -> Your Domain -> DNS -> Records -> Add record`.

1. **Record 1**
   - **Record type**: A
   - **Name**: @
   - **IPv4 address**: 192.0.2.1

2. **Record 2**
   - **Record type**: A
   - **Name**: www
   - **IPv4 address**: 192.0.2.1

3. **Record 3**
   - **Record type**: A
   - **Name**: *
   - **IPv4 address**: 192.0.2.1

### Step 2: Create a Page Rule

- Click `Rules -> Page Rules -> Create Page Rule`.
- In `URL`, enter `*yourdomain.com*` (replace `yourdomain.com` with your actual domain).
- Under `Pick a Setting (required)`, select `Forwarding URL`.
- Under `Select status code (required)`, choose `301`.
- In `Enter destination URL (required)`, enter:  
  `https://sedo.com/search/details/?domain=yourdomain.com`
- Click `Save and Deploy Page Rule`.
- On the pop-up `This rule may not apply to your traffic`, select `Ignore and deploy rule anyway`, then click `Deploy Rule`.

### Step 3: Test the Results

Enter the following in your browser:

- `https://yourdomain.com`
- `https://www.yourdomain.com`
- `https://abc.yourdomain.com`
- `https://yourdomain.com/abcd`
- `http://yourdomain.com`
- `http://www.yourdomain.com`
- `http://abcd.yourdomain.com`
- `http://yourdomain.com/`

If all URLs redirect correctly, the setup is successful.
