# Valentine's Proposal App 💘

A professional and romantic Valentine's Day proposal application built with Vue 3 and Tailwind CSS.

## Features

- **Beautiful Design**: Modern, responsive UI with Tailwind CSS
- **Interactive Elements**: 
  - Animated floating hearts
  - Escaping "No" button that moves when hovered
  - Confetti celebration on success
- **Date Validation**: Only accepts February 14th (Valentine's Day)
- **Form Controls**: Date picker, drink and food preferences
- **Facebook Integration**: Direct link to Facebook profile

## Getting Started

### Prerequisites

- Node.js (version 16 or higher)
- npm or yarn

### Installation

1. Clone or download the project
2. Navigate to the project directory
3. Install dependencies:

```bash
npm install
```

### Development

Start the development server:

```bash
npm run dev
```

The app will be available at `http://localhost:3000`

### Building for Production

Create an optimized production build:

```bash
npm run build
```

### Preview Production Build

Preview the production build locally:

```bash
npm run preview
```

## Project Structure

```
├── src/
│   ├── App.vue          # Main application component
│   ├── main.js          # Application entry point
│   └── style.css        # Global styles and Tailwind imports
├── public/              # Static assets
├── index.html           # HTML template
├── package.json         # Dependencies and scripts
├── tailwind.config.js   # Tailwind CSS configuration
├── vite.config.js       # Vite build configuration
└── README.md            # This file
```

## Technologies Used

- **Vue 3** - Progressive JavaScript framework
- **Vite** - Fast build tool and development server
- **Tailwind CSS** - Utility-first CSS framework
- **canvas-confetti** - Confetti animation library

## Customization

### Changing Colors

Edit `tailwind.config.js` to customize the Valentine's theme colors:

```javascript
theme: {
  extend: {
    colors: {
      'valentine-pink': '#ff3366',
      'valentine-light': '#ffd6e8',
      'valentine-bg': '#fff0f6'
    }
  }
}
```

### Facebook Link

Update the Facebook URL in `src/App.vue`:

```javascript
const openFacebook = () => {
  window.open("YOUR_FACEBOOK_URL", "_blank")
}
```

## Deployment

This app can be deployed to any static hosting service:

- **Vercel**
- **Netlify**
- **GitHub Pages**
- **Firebase Hosting**

Simply run `npm run build` and deploy the contents of the `dist` folder.

## License

MIT License - feel free to use this for your own Valentine's proposals! 💕