# Markdown Previewer

A sleek and modern Markdown Previewer application built using Vite, Vue, and SCSS. This project provides a real-time markdown editing and preview experience, perfect for writers, developers, and anyone working with markdown.

## Features

1. **Real-Time Preview:** See changes in your markdown reflected instantly in the preview pane.
2. **Custom Styling:** Built with SCSS for easy customization of themes and layouts.
3. **Markdown Syntax Support:** Full support for GitHub-flavored markdown, including tables, code blocks, and inline formatting.
4. **Responsive Design:** Optimized for mobile, tablet, and desktop devices.
5. **Lightweight and Fast:** Powered by Vite for blazing-fast development and build processes.
6. **Extensible**: Add custom markdown plugins or extend functionality to suit your workflow.

## How Does It Work?

This application uses the Vue framework to handle dynamic rendering and reactivity. It parses markdown input using a markdown parser (such as [marked](https://marked.js.org/)) and displays the rendered HTML in a styled preview pane.

### Key Features Include

- **Two-Pane Interface:** Edit markdown on the left, preview the rendered output on the right.
- **Live Updates:** Every change you make to the markdown reflects instantly.
- **SCSS Theming:** Customize the app's appearance with modular SCSS.

## Screenshot

![preview](https://github.com/user-attachments/assets/0eb9dabe-ce17-49ec-8dd0-e7a9098ca6cc)

## Installation

Follow these steps to set up the project locally:

```bash
# Clone the repository
git clone https://github.com/ryzmdn/markdown-previewer.git

# Change into the project directory
cd markdown-previewer

# Install dependencies
npm install

# Open the code editor
code .

# Run the development server
npm run dev
```

## Usage

Once the development server is running, access the application at `http://localhost:5173/`. Start editing markdown in the text editor pane and see the real-time preview on the right.

## Customization

1. **Modify Styles**
    - Update SCSS files in the src/styles directory to create custom themes.
2. **Add Features**
    - Extend functionality by adding support for additional markdown syntax or plugins.
3. **Deploy**
    - Deploy the application to platforms like [Vercel](https://vercel.com/), [Netlify](https://www.netlify.com/), or any other service supporting static sites.

## Feedback

We value your input! For suggestions, feature requests, or bug reports, please contact us at `riybuzniz@gmail.com`.

## License

This project is licensed under the **MIT License**. Feel free to use, modify, and distribute it for both personal and commercial purposes.
