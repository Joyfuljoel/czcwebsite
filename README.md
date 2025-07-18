# Firebase Archive Center

A modern, responsive web application for managing church archives including sermons, pictures, important files, and other documents. Built with Firebase Realtime Database and Storage, featuring a beautiful green theme and secure admin functionality.

## Features

### 🔐 Admin Features (Code: CZC2025)
- **Secure Admin Access**: Protected with admin code `CZC2025`
- **File Upload**: Drag & drop or browse to upload multiple files
- **File Management**: Edit, delete, and organize files
- **Category Management**: Organize files into Sermons, Pictures, Important Files, and Others
- **Progress Tracking**: Real-time upload progress indicators

### 👥 Public Features
- **Browse Archives**: View files organized by category
- **Search Functionality**: Search files by title and description
- **Download Files**: Direct download of any file
- **Image Gallery**: Preview images in full-screen modal
- **Audio Player**: Built-in player for sermon audio files
- **Responsive Design**: Works perfectly on desktop, tablet, and mobile

### 🎨 Design Features
- **Green Theme**: Beautiful, church-appropriate green color scheme
- **Modern UI**: Clean, professional interface using Tailwind CSS
- **Interactive Elements**: Hover effects, animations, and transitions
- **Accessibility**: Screen reader friendly with proper ARIA labels

## Setup Instructions

### 1. Firebase Project Setup

1. **Create Firebase Project**:
   - Go to [Firebase Console](https://console.firebase.google.com/)
   - Click "Create a project"
   - Enter project name (e.g., "church-archive")
   - Follow the setup wizard

2. **Enable Realtime Database**:
   - In Firebase Console, go to "Realtime Database"
   - Click "Create Database"
   - Choose "Start in test mode" (for development)
   - Select your preferred location

3. **Enable Storage**:
   - Go to "Storage" in Firebase Console
   - Click "Get started"
   - Choose "Start in test mode"
   - Select your preferred location

4. **Get Configuration Details**:
   - Go to Project Settings (gear icon)
   - Scroll down to "Your apps" section
   - Click "Web" icon to add a web app
   - Register your app name
   - Copy the configuration object

### 2. Database Security Rules

Set up security rules for Realtime Database:

```json
{
  "rules": {
    "files": {
      ".read": true,
      ".write": false,
      "$fileId": {
        ".write": "auth != null"
      }
    }
  }
}
```

### 3. Storage Security Rules

Set up security rules for Storage:

```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

### 4. Application Setup

1. **Download the Files**:
   - Download `firebase-archive.html`
   - Place it in your web server directory

2. **Configure Firebase**:
   - Open the application in your browser
   - You'll see a Firebase Configuration modal
   - Enter your Firebase project details:
     - **Database URL**: `https://your-project-default-rtdb.firebaseio.com/`
     - **Project ID**: Your Firebase project ID
     - **Storage Bucket**: `your-project.appspot.com`
     - **API Key**: Your web API key from Firebase config

3. **Test the Application**:
   - The configuration is saved locally
   - Try accessing admin panel with code `CZC2025`
   - Upload a test file to verify everything works

## File Structure

```
/
├── firebase-archive.html      # Main application file
├── README.md                 # This file
└── html-files/              # Existing HTML files (optional)
    ├── archives.html        # Original archive file
    └── ...
```

## Usage Guide

### For Administrators

1. **Access Admin Panel**:
   - Click "Admin Panel" button
   - Enter code: `CZC2025`

2. **Upload Files**:
   - Select category (Sermons, Pictures, Important Files, Others)
   - Enter title and optional description
   - Drag & drop files or click browse
   - Click "Upload Files"

3. **Manage Files**:
   - View all uploaded files in the management table
   - Edit file titles by clicking the edit icon
   - Delete files by clicking the trash icon
   - Filter by category using the dropdown

### For Users

1. **Browse Files**:
   - Use tabs to switch between categories
   - Click on images to view in full screen
   - Use search bar to find specific files

2. **Download Files**:
   - Click the download button on any file card
   - Files will download directly to your device

## Customization

### Changing the Admin Code

To change the admin code from `CZC2025`:

1. Open `firebase-archive.html`
2. Find line: `if (code === 'CZC2025') {`
3. Replace `CZC2025` with your desired code
4. Save the file

### Styling Modifications

The application uses Tailwind CSS classes. To modify colors:

- **Green theme colors**: Look for classes like `bg-green-600`, `text-green-800`, etc.
- **Custom CSS**: Modify the `<style>` section in the HTML file

### Adding New Categories

To add new file categories:

1. Add option to category select elements:
   ```html
   <option value="new-category">New Category</option>
   ```

2. Add tab button:
   ```html
   <button class="tab-btn" data-tab="new-category">
       <i class="fas fa-icon mr-2"></i>New Category
   </button>
   ```

3. Add tab content section:
   ```html
   <div id="new-category" class="tab-content">
       <h2 class="text-2xl font-bold text-green-800 mb-6">New Category</h2>
       <div id="newCategoryGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
       </div>
   </div>
   ```

## Troubleshooting

### Common Issues

1. **Firebase Configuration Error**:
   - Double-check all configuration values
   - Ensure Database and Storage are enabled
   - Verify security rules are set

2. **Upload Failures**:
   - Check file size limits (Firebase has 32MB limit for Realtime Database)
   - Verify internet connection
   - Check browser console for error messages

3. **Files Not Loading**:
   - Verify Database URL is correct
   - Check if there's data in your Firebase Realtime Database
   - Ensure security rules allow reading

### Browser Support

- Chrome 70+
- Firefox 65+
- Safari 12+
- Edge 79+

## Security Considerations

1. **Admin Code**: Change the default admin code `CZC2025`
2. **Authentication**: Consider implementing proper Firebase Authentication for production
3. **File Types**: Add file type validation as needed
4. **Rate Limiting**: Implement upload rate limiting for production use

## Contributing

To contribute to this project:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## Support

For support or questions:

1. Check the troubleshooting section
2. Review Firebase documentation
3. Check browser console for error messages
4. Verify all setup steps are completed

## License

This project is open source and available under the MIT License.

---

**Note**: This application is designed for church archives and includes features specifically for managing sermons, church documents, and related files. The green theme and admin functionality are tailored for church use but can be customized for other organizations.