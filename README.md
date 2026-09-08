# CrazVerse onboarding

The static onboarding page is built on Firebase Authentication (Google) and Cloud Firestore.

## Production launch checklist

1. In **Firebase Authentication → Sign-in method**, enable the Google provider and set a public support email.
2. In **Firebase Authentication → Settings → Authorized domains**, add the exact production domain(s) that host this page. Remove domains that are not used.
3. Create Firestore in production mode, then deploy the included rules:

   ```bash
   firebase deploy --only firestore:rules
   ```

4. Serve `index.html` over HTTPS. Firebase pop-up authentication must not be launched from `file://`.
5. Review the included Terms of Play and Privacy Policy with legal counsel and publish approved versions before launch.

## Data model

- `players/{uid}` holds the signed-in player profile.
- `usernames/{username}` is an immutable username claim.

The client uses a Firestore transaction to create both documents. The security rules require both documents to agree, which prevents a user from reserving extra usernames or taking a username that is already claimed.



Install Node.js 18+ first. Then run these commands from the repository root:

```bash
npm install --global wrangler
wrangler login
wrangler pages project create crazverse --production-branch main
wrangler pages deploy . --project-name crazverse --branch main
```

