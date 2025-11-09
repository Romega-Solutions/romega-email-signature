# Email Signature Creator# Email Signature Creator

A modern, responsive email signature generator built with Astro and Tailwind CSS, specifically designed for **Romega Solutions** team members. Create professional, branded email signatures with live preview and download functionality.A modern, responsive email signature generator built with Astro and Tailwind CSS, specifically designed for **Romega Solutions** team members. Create professional, branded email signatures with live preview and download functionality.

![Email Signature Creator Preview](./preview.png)![Email Signature Creator Preview](./preview.png)

## 🚀 Features## 🚀 Features

- **Live Preview**: See changes in real-time as you type- **Live Preview**: See changes in real-time as you type

- **Responsive Design**: Signature adapts to different screen sizes- **Responsive Design**: Signature adapts to different screen sizes

- **Download as Image**: Export your signature as a PNG file- **Download as Image**: Export your signature as a PNG file

- **Send to Email**: Automatically send your signature directly to your email inbox- **Send to Email**: Automatically send your signature directly to your email inbox

- **Romega Branding**: Pre-configured with official Romega Solutions branding and colors- **Romega Branding**: Pre-configured with official Romega Solutions branding and colors

- **Easy Customization**: Simple form-based input for all signature fields- **Easy Customization**: Simple form-based input for all signature fields

- **Step-by-Step Guide**: Integrated tutorial with video and written instructions- **Step-by-Step Guide**: Integrated tutorial with video and written instructions

- **Team Directory**: Quick access to Romega Solutions team contact information- **Team Directory**: Quick access to Romega Solutions team contact information

## 🏗️ Project Structure## 🏗️ Project Structure

`text`text

//

├── public/├── public/

│ ├── favicon.svg│ ├── favicon.svg

│ └── romega-logo.svg # Romega Solutions logo│ └── assets/

├── src/│ └── astro.svg # Default logo

│ ├── components/├── src/

│ │ ├── BaseSignature.astro # Main signature card component│ ├── components/

│ │ ├── ControlsForm.astro # Form for user input│ │ ├── BaseSignature.astro # Main signature card component

│ │ ├── DownloadButtons.astro # Download & email functionality│ │ ├── ControlsForm.astro # Form for user input

│ │ ├── SignaturePreview.astro # Preview wrapper│ │ ├── DownloadButtons.astro # Download functionality

│ │ └── Welcome.astro # Main page layout│ │ ├── SignaturePreview.astro # Preview wrapper

│ ├── layouts/│ │ └── Welcome.astro # Main page layout

│ │ └── Layout.astro # Base HTML layout│ ├── layouts/

│ ├── pages/│ │ └── Layout.astro # Base HTML layout

│ │ └── index.astro # Entry point│ ├── pages/

│ └── styles/│ │ └── index.astro # Entry point

│ └── global.css # Tailwind CSS imports│ └── styles/

├── docs/│ └── global.css # Tailwind CSS imports

│ └── N8N_SETUP_GUIDE.md # Email integration guide├── astro.config.mjs # Astro configuration

├── astro.config.mjs # Astro configuration├── tailwind.config.js # Tailwind configuration

├── tailwind.config.js # Tailwind configuration (Romega theme)└── package.json

└── package.json```

````

## 🧞 Commands

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |

| Command                   | Action                                           || :------------------------ | :----------------------------------------------- |

| :------------------------ | :----------------------------------------------- || `npm install`             | Installs dependencies                            |

| `npm install`             | Installs dependencies                            || `npm run dev`             | Starts local dev server at `localhost:4321`      |

| `npm run dev`             | Starts local dev server at `localhost:4321`      || `npm run build`           | Build your production site to `./dist/`          |

| `npm run build`           | Build your production site to `./dist/`          || `npm run preview`         | Preview your build locally, before deploying     |

| `npm run preview`         | Preview your build locally, before deploying     || `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |

| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` || `npm run astro -- --help` | Get help using the Astro CLI                     |

| `npm run astro -- --help` | Get help using the Astro CLI                     |

## 🛠️ Tech Stack

## 🛠️ Tech Stack

- **[Astro](https://astro.build)** - Web framework for content-driven websites

- **[Astro](https://astro.build)** - Web framework for content-driven websites- **[Tailwind CSS](https://tailwindcss.com)** - Utility-first CSS framework

- **[Tailwind CSS](https://tailwindcss.com)** - Utility-first CSS framework- **[html-to-image](https://github.com/bubkoo/html-to-image)** - Generate images from DOM nodes

- **[html-to-image](https://github.com/bubkoo/html-to-image)** - Generate images from DOM nodes- **[Lucide Icons](https://lucide.dev)** - Beautiful open-source icon library

- **[Lucide Icons](https://lucide.dev)** - Beautiful open-source icon library- **[n8n](https://n8n.io)** - Workflow automation for email sending (optional)

- **[n8n](https://n8n.io)** - Workflow automation for email sending (optional)- **TypeScript** - Type-safe JavaScript

- **TypeScript** - Type-safe JavaScript

## 🎨 Color Scheme

## 🎨 Color Scheme

The project uses the **official Romega Solutions design system** defined in `tailwind.config.js`:

The project uses the **official Romega Solutions design system** defined in `tailwind.config.js`:

### Primary Colors

### Primary Colors

- **Primary**: `#0069D9` - Official Romega brand blue

- **Primary**: `#0069D9` - Official Romega brand blue- **Accent**: `#D97B00` - Official Romega accent orange

- **Accent**: `#D97B00` - Official Romega accent orange- **Neutral**: Grayscale palette for backgrounds and text

- **Neutral**: Grayscale palette for backgrounds and text

### Custom Prefix

### Custom Prefix

All Romega-specific colors use the `rs-` (Romega Solutions) prefix:

All Romega-specific colors use the `rs-` (Romega Solutions) prefix:

- `bg-rs-primary-500` - Primary background

- `bg-rs-primary-500` - Primary background- `text-rs-accent-600` - Accent text

- `text-rs-accent-600` - Accent text- `border-rs-neutral-200` - Neutral borders

- `border-rs-neutral-200` - Neutral borders

**Note**: This color system is proprietary to Romega Solutions and should not be modified to maintain brand consistency.

**Note**: This color system is proprietary to Romega Solutions and should not be modified to maintain brand consistency.

## 📝 How to Use (Romega Team Members)

## 📝 How to Use (Romega Team Members)

1. **Fill out the form** with your Romega information:

1. **Fill out the form** with your Romega information:

   - Full Name

   - Full Name   - Job Title at Romega Solutions

   - Job Title at Romega Solutions   - Romega Phone Number

   - Romega Phone Number   - Official @romega-solutions.com Email Address

   - Official @romega-solutions.com Email Address

2. **See live preview** as you type - the signature updates in real-time with Romega branding

2. **See live preview** as you type - the signature updates in real-time with Romega branding

3. **Get your signature** using one of two methods:

3. **Get your signature** using one of two methods:

   - **Download as Image**: Click to download your signature as a PNG file

   - **Download as Image**: Click to download your signature as a PNG file   - **Send to Email**: Click to receive your signature directly in your Romega inbox

   - **Send to Email**: Click to receive your signature directly in your Romega inbox

4. **Set up in Gmail** by following the integrated step-by-step guide with video tutorial

4. **Set up in Gmail** by following the integrated step-by-step guide with video tutorial

## 🎯 Customization

## 🎯 Customization (For Developers)

### Adding New Fields

### Adding New Fields

1. Update `defaultData` in `Welcome.astro`

1. Update `defaultData` in `Welcome.astro`2. Add input field in `ControlsForm.astro`

2. Add input field in `ControlsForm.astro`3. Add display element in `BaseSignature.astro` with `data-field="fieldname"`

3. Add display element in `BaseSignature.astro` with `data-field="fieldname"`4. Update the `fields` array in the sync script

4. Update the `fields` array in the sync script

### Styling Changes

### Styling Changes

- Modify Tailwind classes using the `rs-` prefix

- Modify Tailwind classes using the `rs-` prefix- Update colors in `tailwind.config.js`

- Update colors in `tailwind.config.js`- Add custom CSS in `global.css`

- Add custom CSS in `global.css`- Update fonts by modifying the Google Fonts import

- Update fonts by modifying the Google Fonts import

### Email Integration Setup

### Email Integration Setup

To enable the "Send to Email" feature with n8n:

To enable the "Send to Email" feature with n8n:

1. **Set up n8n workflow** - See `docs/N8N_SETUP_GUIDE.md` for detailed instructions

1. **Set up n8n workflow** - See `docs/N8N_SETUP_GUIDE.md` for detailed instructions2. **Update environment variables**:

2. **Update environment variables**:   ```bash

   ```bash   # .env

   # .env   PUBLIC_N8N_WEBHOOK_URL=https://n8n.yourdomain.com/webhook/email-signature

   PUBLIC_N8N_WEBHOOK_URL=https://n8n.yourdomain.com/webhook/email-signature   PUBLIC_N8N_AUTH_TOKEN=your-secret-token-here

   PUBLIC_N8N_AUTH_TOKEN=your-secret-token-here   ```

   ```3. **Update `DownloadButtons.astro`** with your webhook URL and auth token

3. **Update `DownloadButtons.astro`** with your webhook URL and auth token

For now, the "Send to Email" button downloads the image locally. Follow the n8n setup guide to enable actual email sending.

For now, the "Send to Email" button downloads the image locally. Follow the n8n setup guide to enable actual email sending.

## 📱 Responsive Design

## 📧 Email Sending Setup

The signature is designed to be responsive and will:

The application includes a "Send to Email" feature that can be configured with n8n workflow automation.

- Stack vertically on mobile devices

### Current Functionality (Default)- Maintain readability across all screen sizes

- Adapt container width based on content length

- Clicking "Send to Email" generates and downloads the signature- Handle long text with proper word wrapping

- Shows a success dialog for demonstration purposes

## 🤝 Contributing

### Production Setup

1. Fork the repository

For automatic email delivery:2. Create a feature branch (`git checkout -b feature/amazing-feature`)

3. Commit your changes (`git commit -m 'Add amazing feature'`)

1. Install and configure n8n on your server4. Push to the branch (`git push origin feature/amazing-feature`)

2. Create the email workflow (webhook → process image → send email)5. Open a Pull Request

3. Update the webhook URL in `DownloadButtons.astro`

4. Add authentication token for security## 📄 License



**Full setup guide**: See `docs/N8N_SETUP_GUIDE.md` for step-by-step instructionsThis project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.



## 📱 Responsive Design## � Email Sending Setup



The signature is designed to be responsive and will:The application includes a "Send to Email" feature that can be configured with n8n workflow automation.



- Stack vertically on mobile devices### Current Functionality (Default)

- Maintain readability across all screen sizes

- Provide an optimal viewing experience on desktop and mobile- Clicking "Send to Email" generates and downloads the signature

- Handle long text with proper word wrapping- Shows a success dialog for demonstration purposes



## 🚀 Deployment### Production Setup



Build the static site:For automatic email delivery:



```bash1. Install and configure n8n on your server

npm run build2. Create the email workflow (webhook → process image → send email)

```3. Update the webhook URL in `DownloadButtons.astro`

4. Add authentication token for security

The output will be in the `dist/` directory, ready to deploy to:

**Full setup guide**: See `docs/N8N_SETUP_GUIDE.md` for step-by-step instructions

- Netlify

- Vercel## 📱 Responsive Design

- GitHub Pages

- Any static hosting serviceThe signature is designed to be responsive and will:



## 🤝 Contributing- Stack vertically on mobile devices

- Maintain readability across all screen sizes

This is a proprietary tool created exclusively for **Romega Solutions**. - Provide an optimal viewing experience on desktop and mobile

- Handle long text with proper word wrapping

**For Romega Team Members:**

- Report issues or suggest improvements to the IT team## 🚀 Deployment

- Contact Ken Patrick Garcia for feature requests or modifications

Build the static site:

**External Contributors:**

- This repository is private and proprietary to Romega Solutions```bash

- Unauthorized use, modification, or distribution is prohibitednpm run build

````

## 📄 License

The output will be in the `dist/` directory, ready to deploy to:

This project is proprietary software owned by **Romega Solutions**. All rights reserved.

- Netlify

This tool is intended for internal use by Romega Solutions team members only. Unauthorized use, copying, modification, or distribution of this software is strictly prohibited.- Vercel

- GitHub Pages

## 👀 Resources- Any static hosting service

- [Astro Documentation](https://docs.astro.build)## 🤝 Contributing

- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

- [html-to-image Documentation](https://github.com/bubkoo/html-to-image)1. Fork the repository

- [n8n Documentation](https://docs.n8n.io)2. Create a feature branch (`git checkout -b feature/amazing-feature`)

- [Lucide Icons](https://lucide.dev)3. Commit your changes (`git commit -m 'Add amazing feature'`)

4. Push to the branch (`git push origin feature/amazing-feature`)

---5. Open a Pull Request

**Built with ❤️ by Ken Patrick Garcia for [Romega Solutions](https://www.romega-solutions.com)**## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## �👀 Want to learn more?

- [Astro Documentation](https://docs.astro.build)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [html-to-image Documentation](https://github.com/bubkoo/html-to-image)
- [n8n Documentation](https://docs.n8n.io)
- [Lucide Icons](https://lucide.dev)

---

**Built with ❤️ by Ken Patrick Garcia for [Romega Solutions](https://www.romega-solutions.com)**
