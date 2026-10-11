APPLEX MODDERS ADMIN PANEL — setup notes

Files:
- admin.html: splash, Firebase Authentication login, dashboard, banner upload, download URL, maintenance mode, announcement, timer setting, local music player.
- assets/: artwork references
- firestore.rules.example and storage.rules.example: example secure rules
- Existing main website is separate; it must read the same Firestore document and use bannerUrl, downloadUrl, siteTitle, announcement, timerSeconds, maintenance and maintenanceMessage to reflect admin changes.

IMPORTANT LOGIN SECURITY:
The requested email is prefilled as applexadmin@gmail.com. Do NOT hardcode a password in HTML. The password string previously suggested by the user is not embedded. Create the admin user in Firebase Console > Authentication > Users, set a strong password, and enable Email/Password sign-in. This page authenticates against Firebase Auth.

Device-specific owner label:
The page uses user-agent model matching as a cosmetic label only. Browser device strings may be hidden or spoofed, so it is NOT security. Real authorization comes from Firebase Auth and rules.

Firebase setup:
1. Open Firebase Console for project proxyprojectv5-5c8dd.
2. Enable Authentication > Sign-in method > Email/Password.
3. Create admin user applexadmin@gmail.com with a secure password you control.
4. Enable Firestore Database and Storage.
5. In Authentication > Users, copy the admin UID. Replace YOUR_ADMIN_FIREBASE_UID in both example rules with that UID, then publish rules.
6. Host on HTTPS (Firebase Hosting recommended). ES modules generally do not work correctly when opening the file directly with file://.
7. Main website must subscribe/read siteConfig/public. For live updates use onSnapshot(doc(db,'siteConfig','public'), ...) and render the fields listed above.
8. Save settings from admin; check browser console if rules or service setup rejects a write.

Music:
The player plays an audio file selected locally by the admin in their current browser session. No song is bundled or uploaded; use audio you have permission to play.
