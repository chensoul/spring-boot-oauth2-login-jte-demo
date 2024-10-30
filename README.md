# Spring Boot OAuth2 Login Demo

This project demonstrates how to implement OAuth2 authentication in a Spring Boot application using custom login pages
with JTE (Java Template Engine) and Tailwind CSS. It includes both traditional form login and OAuth2 login with Google
and GitHub.

## Features

- Custom login page using JTE and Tailwind CSS
- Traditional username/password authentication
- OAuth2 authentication with Google and GitHub
- Secure logout functionality
- CSRF protection

## Prerequisites

- Java 17+
- Maven
- Google account (for Google OAuth)
- GitHub account (for GitHub OAuth)

## Quick Start

1. Clone the repository

```bash
git clone <repository-url>
cd spring-boot-oauth2-login-jte-demo
```

2. Configure OAuth credentials (see OAuth Setup sections below)

3. Set environment variables

```bash
export GOOGLE_CLIENT_ID=your_google_client_id
export GOOGLE_CLIENT_SECRET=your_google_client_secret
export GITHUB_CLIENT_ID=your_github_client_id
export GITHUB_CLIENT_SECRET=your_github_client_secret
```

4. Run the application

```bash
mvn spring-boot:run
```

5. Visit http://localhost:8080

## Default User Credentials

The application comes with a default user for testing:

- Username: `user`
- Password: `pass`

## Google OAuth2 Setup

1. Go to [Google Cloud Console](https://console.cloud.google.com/)

2. Create a new project or select an existing one

3. Configure the OAuth consent screen:
    - Go to "APIs & Services" > "OAuth consent screen"
    - Choose "External" user type
    - Fill in required information:
        - App name
        - User support email
        - Developer contact information
    - Add scopes: email, profile, openid
    - Add test users if using external user type

4. Create OAuth2 credentials:
    - Go to "APIs & Services" > "Credentials"
    - Click "Create Credentials" > "OAuth client ID"
    - Choose "Web application"
    - Add these URLs:
      ```
      Authorized JavaScript origins:
      http://localhost:8080
 
      Authorized redirect URIs:
      http://localhost:8080/login/oauth2/code/google
      ```
    - Note your client ID and client secret

## GitHub OAuth Setup

1. Go to [GitHub Developer Settings](https://github.com/settings/developers)

2. Click "New OAuth App"

3. Fill in the application details:
   ```
   Application name: Your App Name
   Homepage URL: http://localhost:8080
   Authorization callback URL: http://localhost:8080/login/oauth2/code/github
   ```

4. Register the application

5. Note your client ID and generate a client secret

## Troubleshooting

### OAuth2 Issues

1. Redirect URI Mismatch
    - Verify the exact URIs in your OAuth provider settings
    - For Google: `http://localhost:8080/login/oauth2/code/google`
    - For GitHub: `http://localhost:8080/login/oauth2/code/github`
    - No trailing slashes
    - Correct protocol (http/https)
    - Correct port number

2. Authentication Errors
    - Clear browser cookies and cache
    - Check environment variables are set correctly
    - Verify OAuth provider console settings
    - Check application logs for detailed error messages

### Common Issues

1. Login Page Not Loading
    - Verify JTE configuration
    - Check template paths
    - Clear browser cache

2. Authentication Not Working
    - Verify default user credentials
    - Check OAuth configuration
    - Ensure CSRF token is present in forms

## Security Considerations

1. Production Deployment
    - Use HTTPS
    - Update OAuth redirect URIs for production domain
    - Secure client secrets
    - Enable CSRF protection
    - Consider session management settings

2. OAuth Provider Setup
    - Restrict OAuth scopes to minimum required
    - Verify redirect URIs
    - Protect client secrets
    - Use environment variables
