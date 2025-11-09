# Email Signature Creator

A modern, responsive email signature generator built with Astro and Tailwind CSS. Create professional email signatures with live preview and download functionality.

![Email Signature Creator Preview](./preview.png)

## 🚀 Features

- **Live Preview**: See changes in real-time as you type
- **Responsive Design**: Signature adapts to different screen sizes
- **Download as Image**: Export your signature as a PNG file
- **Send to Email**: Automatically send your signature directly to your email inbox
- **Professional Layout**: Clean, modern design with company branding
- **Easy Customization**: Simple form-based input for all signature fields
- **Step-by-Step Guide**: Integrated tutorial with video and written instructions
- **Team Directory**: Quick access to company contact information

## 🏗️ Project Structure

```text
/
├── public/
│   ├── favicon.svg
│   └── assets/
│       └── astro.svg          # Default logo
├── src/
│   ├── components/
│   │   ├── BaseSignature.astro     # Main signature card component
│   │   ├── ControlsForm.astro      # Form for user input
│   │   ├── DownloadButtons.astro   # Download functionality
│   │   ├── SignaturePreview.astro  # Preview wrapper
│   │   └── Welcome.astro           # Main page layout
│   ├── layouts/
│   │   └── Layout.astro            # Base HTML layout
│   ├── pages/
│   │   └── index.astro             # Entry point
│   └── styles/
│       └── global.css              # Tailwind CSS imports
├── astro.config.mjs                # Astro configuration
├── tailwind.config.js              # Tailwind configuration
└── package.json
```

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## 🛠️ Tech Stack

- **[Astro](https://astro.build)** - Web framework for content-driven websites
- **[Tailwind CSS](https://tailwindcss.com)** - Utility-first CSS framework
- **[html-to-image](https://github.com/bubkoo/html-to-image)** - Generate images from DOM nodes
- **[Lucide Icons](https://lucide.dev)** - Beautiful open-source icon library
- **[n8n](https://n8n.io)** - Workflow automation for email sending (optional)
- **TypeScript** - Type-safe JavaScript

## 🎨 Color Scheme

The project uses the Romega Solutions design system defined in `tailwind.config.js`:

### Primary Colors

- **Primary**: `#0069D9` - Main brand color (blue)
- **Accent**: `#D97B00` - Secondary accent color (orange)
- **Neutral**: Grayscale palette for backgrounds and text

### Custom Prefix

All custom colors use the `rs-` prefix:

- `bg-rs-primary-500` - Primary background
- `text-rs-accent-600` - Accent text
- `border-rs-neutral-200` - Neutral borders

## 📝 How to Use

1. **Fill out the form** with your information:

   - Full Name
   - Job Title
   - Phone Number
   - Email Address

2. **See live preview** as you type - the signature updates in real-time

3. **Get your signature** using one of two methods:

   - **Download as Image**: Click to download your signature as a PNG file
   - **Send to Email**: Click to receive your signature directly in your inbox

4. **Set up in Gmail** by following the integrated step-by-step guide with video tutorial

## 🎯 Customization

### Adding New Fields

1. Update `defaultData` in `Welcome.astro`
2. Add input field in `ControlsForm.astro`
3. Add display element in `BaseSignature.astro` with `data-field="fieldname"`
4. Update the `fields` array in the sync script

### Styling Changes

- Modify Tailwind classes using the `rs-` prefix
- Update colors in `tailwind.config.js`
- Add custom CSS in `global.css`
- Update fonts by modifying the Google Fonts import

### Email Integration Setup

To enable the "Send to Email" feature with n8n:

1. **Set up n8n workflow** - See `docs/N8N_SETUP_GUIDE.md` for detailed instructions
2. **Update environment variables**:
   ```bash
   # .env
   PUBLIC_N8N_WEBHOOK_URL=https://n8n.yourdomain.com/webhook/email-signature
   PUBLIC_N8N_AUTH_TOKEN=your-secret-token-here
   ```
3. **Update `DownloadButtons.astro`** with your webhook URL and auth token

For now, the "Send to Email" button downloads the image locally. Follow the n8n setup guide to enable actual email sending.

## 📱 Responsive Design

The signature is designed to be responsive and will:

- Stack vertically on mobile devices
- Maintain readability across all screen sizes
- Adapt container width based on content length
- Handle long text with proper word wrapping

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## � Email Sending Setup

The application includes a "Send to Email" feature that can be configured with n8n workflow automation.

### Current Functionality (Default)

- Clicking "Send to Email" generates and downloads the signature
- Shows a success dialog for demonstration purposes

### Production Setup

For automatic email delivery:

1. Install and configure n8n on your server
2. Create the email workflow (webhook → process image → send email)
3. Update the webhook URL in `DownloadButtons.astro`
4. Add authentication token for security

**Full setup guide**: See `docs/N8N_SETUP_GUIDE.md` for step-by-step instructions

## 📱 Responsive Design

The signature is designed to be responsive and will:

- Stack vertically on mobile devices
- Maintain readability across all screen sizes
- Provide an optimal viewing experience on desktop and mobile
- Handle long text with proper word wrapping

## 🚀 Deployment

Build the static site:

```bash
npm run build
```

The output will be in the `dist/` directory, ready to deploy to:

- Netlify
- Vercel
- GitHub Pages
- Any static hosting service

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## �👀 Want to learn more?

- [Astro Documentation](https://docs.astro.build)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [html-to-image Documentation](https://github.com/bubkoo/html-to-image)
- [n8n Documentation](https://docs.n8n.io)
- [Lucide Icons](https://lucide.dev)

---

**Built with ❤️ by Ken Patrick Garcia for [Romega Solutions](https://www.romega-solutions.com)**
