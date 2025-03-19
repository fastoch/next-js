# Next.js 15 Crash Course (Oct 2024)

Build and Deploy a Production-Ready Full Stack App (by JS Mastery).  
https://www.youtube.com/watch?v=Zq5fmkH0T78  

# Intro

In **2013**, Facebook introduced **React**, a groundbreaking technology that revolutionized web development.  

React is primarily a **frontend** library designed for building user interfaces.  
It is widely used in web development to create dynamic and interactive UI components.  
React focuses on rendering views efficiently using its virtual DOM and a component-based architecture.  

However, React can also be utilized in **backend**-related tasks when combined with frameworks like **Next**.js or **Gatsby**.js.  
These frameworks extend React's capabilities to handle server-side logic, making it possible to build **full-stack** applications.  

Here's what the official React documentation says:  
![image](https://github.com/user-attachments/assets/062b81cd-b3fa-464c-94af-3790ca078473)  

## What we'll build

A full stack Next.js application.  

Our own version of Y Combinator (YC), the famous startup accelerator.  
- We'll allow users to create and share their startup with the world.  
- Once they submit it, it appears instantly without needing to reload the page.  
- They can also search by title, username, or category to get instant results.
- Once you find the startup you like, you can navigate to its details and see how many people have found it interesting
- we'll integrate GitHub authentication via NextAuth.js

We'll implement all that using the latest Next.js features, like:
- Partial Prerendering (PPR)
- next/after
- new forms
- serverComponentsHmrCache
- server actions

We'll also learn how to use the Sanity Content Operating System, an API-based platform for structured content that pairs perfectly with Next.js and other
popular frontend frameworks. Sanity has a generous free-tier and no credit card is required.  

# Next.js Benefits

What does Next.js have that React doesn't?

## Benefit #1: Architecture

Originally, React had 2 types of components: 
- Function components
- Class-based components

But now, components are also categorized by where they run:
- If a component runs in the user's browser, it's called a **client component**
- It it runs on the server, it's called a **server component**

This division was released in React 19 (Dec 2024), and although frameworks like Astro or Remix also support it, Next.js was the first to adopt it and fully utilize it.  

>[!important]
>**Since server components are more performant, Next.js automatically converts every new component you create into a server component**, unless you specifically instruct it not to.

## Benefit #2: The way Next.js handles rendering

While React 19 supports Server components, Next.js extends them to more advanced **rendering strategies**, allowing us to choose exactly where and when they'll be rendered, optimizing the performance even further.  

### Client-side rendering (CSR)

The server sends a minimal HTML file to the browser, which then uses JavaScript to dynamically generate the full page content after it loads in the browser. 
This means that, initially, the HTML source code contains **little to no meaningful content** for search engine crawlers to index.  
Many search engine crawlers either do not execute JavaScript or have limited capabilities to do so...

### Server-side rendering (SSR)

This process involves rendering the web page on the server before transmitting it to the browser.  
When you visit a page, the server processes and renders the components on the server, and sends back fully-rendered HTML and JS code to the client, instantly displaying the website.  

**But why does SSR matter so much?**  
On top of the fact that your website will load in 300 ms, and have PageSpeed insights that look really good, SSR will significantly improve your website's search engine optimization (SEO).  

>[!note]
>PageSpeed Insights is a free online tool developed by Google to analyze and evaluate the performance of web pages on both mobile and desktop devices.

Client-side rendering makes it almost impossible for search engines to crawl and index your websites, as they're completely empty.  
Next.js solves this issue by sending **pre-rendered** code, giving the search engines plenty of stuff to rank us on.   

## Benefit #3: Routing

In React, you need to install an additional React router package to create routes.  
Next.js doesn't require installing a routing package, and uses a much more intuitive approach to routing called **file-based routing**.  

Each folder's name becomes a route's path.  
For example, a folder named 'about' will create a new `/about` route:  
![image](https://github.com/user-attachments/assets/9a1b7d0f-9cbb-421c-a190-4c9a01e652c4)  

## Benefit #4: Serverless Functions

Next.js serverless functions are a powerful feature that allows developers to run backend code without managing or configuring servers.   
- These functions are executed on-demand, triggered by events such as HTTP requests.  
- These functions automatically scale based on demand, eliminating concerns about server capacity.  

In Next.js, serverless functions are implemented as API routes. Each file in the `pages/api` directory corresponds to an API endpoint.  
Using the same file-based routing system we've just described, we can create **serverless functions** to handle backend API requests.  

This means we can create an API endpoint by simply creating a file called `route.js` in a specific folder, without needing to worry about the server infrastructure.  

## Benefit #5: Next.js automates code splitting by default!

And there are many other scaling features that Next.js provides out-of-the-box (OOTB), like **Automatic Code splitting**.  
While code splitting in React is possible, it requires manual configuration, especially as the application grows.  

>[!important]
>**Code splitting** is a technique used in web development to **improve application performance** by breaking down large JavaScript bundles into smaller, more manageable chunks that can be loaded on demand. <br>
>This approach allows applications to load only the code necessary for the current user interaction, rather than loading the entire codebase upfront.

Automatic code splitting means that, when a user navigates to a different page, only the code for that page is loaded, which significantly speeds up page load times.  

## Other performance optimization features

But automatic code splitting is just one out of many built-in performance optimizations that Next.js provides:
- **Font optimization** reduces **layout shift** by pre-loading font files, which improves loading time and enhances the UX
  - it also reduces reliance on external services such as Google Fonts
- **Image optimization** automatically compresses images, and applies **lazy loading**, **CDNs** support, and more
- **Script optimization** even works with third-party scripts 

>[!note]
>**Image lazy loading** is a powerful technique used to optimize website performance by deferring the loading of images until they are needed, typically when they become visible in the user's viewport. <br>

>[!note]
>**Next.js and Content Delivery Networks (CDNs)**: <br>
>https://dev.to/dhrumitdk/nextjs-and-content-delivery-networks-cdns-optimizing-static-assets-for-faster-load-times-206o

## Next.js is the definition of Cutting-Edge 

Next.js supports the latest features, such as:
- **React compiler**: an open-source build-time tool which automatically optimizes React apps for improved performance
- **MDX file integration**: a powerful format that allows you to write JSX in Markdown files
- managing most **SEO-related tags**
- **Analytics** that run without blocking UI
- **HMR**: Hot Module Replacement
- **Fast Refresh**: a React-specific enhancement to HMR
- **Server Components**: allows developers to render UI components on the server
- ...

---

# Let's get practical

- create a new folder named 'next-js' for hosting our first Next.js project, then open this folder in VS Code
- open up a terminal and run `npx create-next-app@latest` to initialize our application
- for the project name, type `./` since we're already in the folder within which we want to create our app
  - /!\ The current folder name must not contain any uppercase characters /!\
- say yes for TypeScript, yes for ESLint, yes for TailwindCSS
- we don't need a /src directory
- say yes to App Router, yes to TurboPack
- we don't need to customize the import alias, the default one is fine

This will create all the necessary files and install the required dependencies.  
Now that our project is set up and ready to go, let's talk about the different files and folders we got here:
- `tsconfig.json`: the config file for TypeScript. It defines what should be type-checked, what should be ignored, and the rules to follow
- `tailwind.config.ts`: where you can add a custom tailwind setup. We can customize colors, sizes, shadows, plugins, etc.
- `README.md`: Markdown file that provides details and explanations about the project
- `postcss.config.mjs`: config file for PostCSS. A tool to process CSS files with different plugins. 
  - In this case, it uses the TailwindCSS plugin, which allows us to use utility-first classes in our CSS files.
- `package.json`: the file that contains all the project dependencies and scripts
  - there's a `dev` script which starts next.js in development mode with HMR enabled, error reporting, and more
  - `build` creates an optimized production build of your app
  - `start` simply starts Next.js in production mode
  - `lint` runs ESLint for all files in the project
- `package-lock.json`: a file that contains the exact version of each dependency and their dependencies, so that everyone working on the project uses the same versions.



@13/323
