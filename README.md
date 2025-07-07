# 🎫 Event QR Code Scanner

A simple, real-time QR code scanning web application designed for event ticket validation. This single-file application uses your device's camera to scan QR codes and validate them against a pre-set list of event codes.

## ✨ Features

- **Real-time QR Code Scanning**: Uses device camera for instant QR code detection
- **Visual Targeting**: Green scanning box with animated corners to help aim the camera
- **Validation System**: Checks scanned codes against valid event tickets
- **Duplicate Prevention**: Tracks used codes to prevent multiple uses
- **Mobile Responsive**: Optimized for smartphones and tablets
- **Camera Permission Handling**: Clear instructions when camera access is denied
- **Scan Cooldown**: Prevents accidental re-scanning with a 2-second pause
- **Visual Feedback**: Animated "ACCEPTED!" and "REFUZAT!" messages

## 🚀 Quick Start

### Option 1: Open Directly
Simply open `index.html` in a modern web browser that supports camera access (Chrome, Firefox, Safari, Edge).

### Option 2: Local Server (Recommended)
For better camera compatibility, especially on mobile devices, serve the file through a local server:

```bash
# Using Python 3
python -m http.server 8000

# Using Python 2
python -m SimpleHTTPServer 8000

# Using Node.js (if you have http-server installed)
npx http-server

# Using PHP
php -S localhost:8000
```

Then visit `http://localhost:8000` in your browser.

## 📱 Usage

1. **Open the Application**: Load the HTML file in your web browser
2. **Grant Camera Permission**: Click "Allow" when prompted for camera access
3. **Start Scanning**: Click the "Start Scanner" button
4. **Aim and Scan**: Point your camera at a QR code within the green targeting box
5. **View Results**: 
   - ✅ **"ACCEPTED!"** - Valid, unused code
   - ❌ **"REFUZAT!"** - Invalid or already used code
6. **Stop When Done**: Click "Stop Scanner" to end the session

## 🔧 Technical Details

### Dependencies
- **jsQR Library**: QR code detection and decoding (loaded from CDN)
- **Modern Browser**: With support for `getUserMedia` API

### Valid Event Codes (Demo)
The application comes with these sample valid codes:
- `EVENT2024-001` through `EVENT2024-005`
- `PREMIUM-VIP-001` and `PREMIUM-VIP-002`
- `GENERAL-ADM-001` through `GENERAL-ADM-003`

### Browser Compatibility
- ✅ Chrome 53+ (Desktop & Mobile)
- ✅ Firefox 36+ (Desktop & Mobile)
- ✅ Safari 11+ (Desktop & Mobile)
- ✅ Edge 12+
- ❌ Internet Explorer (not supported)

## 🚀 Deployment

### GitHub Pages
1. Push this repository to GitHub
2. Go to repository Settings → Pages
3. Select source branch (usually `main`)
4. Your app will be available at `https://yourusername.github.io/repository-name`

### Netlify
1. Connect your GitHub repository to Netlify
2. Deploy with default settings
3. Your app will get a custom Netlify URL

### Vercel
1. Connect your GitHub repository to Vercel
2. Deploy with default settings
3. Automatic deployments on every push

## ⚠️ Security Limitations

**⚠️ IMPORTANT SECURITY NOTICE ⚠️**

This is a **demonstration application** with several security limitations:

### Current Limitations:
1. **Client-Side Validation**: Valid codes are stored in the browser's JavaScript, making them visible to anyone who views the source code
2. **No Server Verification**: All validation happens locally, which can be bypassed
3. **No Persistent Storage**: Used codes are only tracked during the current session
4. **No Authentication**: No user authentication or access control

### Production Security Requirements:
For a production environment, you should:

1. **Server-Side Validation**: 
   - Store valid codes in a secure database
   - Validate codes on the server, not in the browser
   - Use HTTPS for all communications

2. **Authentication System**:
   - Implement user login/authentication
   - Use role-based access control
   - Track which user scanned which code

3. **Database Integration**:
   - Store used codes in a persistent database
   - Implement real-time synchronization across devices
   - Add audit logging for all scans

4. **API Security**:
   - Use secure API endpoints with authentication
   - Implement rate limiting
   - Add input validation and sanitization

## 🛠️ Customization

### Adding More Valid Codes
Edit the `validCodes` Set in the JavaScript section:

```javascript
this.validCodes = new Set([
    'YOUR-EVENT-001',
    'YOUR-EVENT-002',
    // Add more codes here
]);
```

### Changing Messages
Modify the text in the `processQRCode` method:
- Change `'ACCEPTED!'` to your preferred success message
- Change `'REFUZAT!'` to your preferred rejection message

### Styling
The application uses embedded CSS. Modify the styles in the `<style>` section to match your event branding.

## 📋 Requirements

- Modern web browser with camera support
- Device with camera (webcam or mobile camera)
- HTTPS connection (required for camera access on most browsers)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/improvement`)
5. Create a Pull Request

## 📄 License

This project is open source and available under the MIT License.

## 🆘 Troubleshooting

### Camera Not Working
- Ensure you've granted camera permission
- Try refreshing the page
- Check browser settings for camera access
- Use HTTPS instead of HTTP
- Try a different browser

### QR Codes Not Scanning
- Ensure good lighting
- Hold the camera steady
- Make sure the QR code is within the green box
- Try moving closer or further from the QR code
- Clean your camera lens

### Performance Issues
- Close other applications using the camera
- Try using a different browser
- Ensure stable internet connection (for loading the jsQR library)

## 📞 Support

For issues, questions, or contributions, please:
1. Check the troubleshooting section above
2. Search existing GitHub issues
3. Create a new issue with detailed information about your problem

---

**Note**: This application is intended for demonstration and learning purposes. For production use, please implement proper server-side validation and security measures as outlined in the Security Limitations section.