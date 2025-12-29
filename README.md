

In 'app' folder we set different pages that we want on overall website. 'page.js' tells Nextjs that it should render a page ('page.js' a react function and 'page.js' is a server component, Nextjs ensures that 'page.js' is rendered on the server and executed on server, terminal in vscode is running on server) and 'layout.js'. Next.js has server components that are rendered and converted to HTML which is sent to browser. For example need to add a page called 'http://localhost:3000/about' we can do it in 'app' folder by adding the routes in 'app' folder by adding folders in 'app' folder. If we want to add 'http://localhost:3000/about' we need to add 'about' folder inside 'app' folder.  Additionally we need to create a file called 'page.js' inside 'about' folder to render a page.
Next.js have reserved filenames. But filename only matter inside app folder.

page.js - define page content
layout.js - define wrapper around pages
not-found.js - define 'Not found' fallback page 
error.js - define error fallback page
loading.js => Fallback page which is shown whilst sibling or nested pages (or layouts) are fetching data

route.js => Allows you to create an API route (i.e., a page which does NOT return JSX code but instead data, e.g., in the JSON format)

There is a root page inside 'app' folder which defines the content of page inside 'http://localhost:3000' and the file that defines content inside 'http://localhost:3000' is 'page.js' (inside app folder) and this 'page.js' is the root file inside app folder.

The 'page.js' inside the 'about' folder will determine that defines page content inside 'http://localhost:3000/about'.



app/about/page.js


export default function About() {
  return (
    <main >
     <p>About us</p>    
</main>
  );
}


app/page.js

import Link from 'next/link';

export default function Home() {
  return (
    <main >
     <p>About us</p>  
<p><Link to="/about>About Us</Link></p>  
</main>
  );
}


'Link' is used instead of 'a' anchor tag because when the home page is loaded and using anchor tag instead of  'Link' tag will reload and the single page application is not manitained, hence we use 'Link' which will load the content of 'http://localhost:3000/about' from Javascript client code from home page ('http://localhost:3000') will be replacing the UI to ('http://localhost:3000/about') without reloading and maintaining the single page application concept by using 'Link' instead of 'a' anchor tag. If we want to change the UI from one page to another page inside the website we use 'Link' in Nextjs. 

In 'app' folder 'layout.js' defines the shell around one or more pages . Especially 'app/page.js' place as a shell inside the 'app/layout.js'. Every Next.js application require one root 'layout.js' file that's 'app/layout.js'. In 'app/about' we can add 'layout.js' i.e 'app/about/layout.js'. In root 'layout.js' file (i.e app/layout.js) we are also exporting a React component 



app/layout.js


import './global.css';

export const metadata = {
title: 'NextJS course app',
description: 'Your first Nextjs app!'
};

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}


This 'app/layout.js' has a standard children prop (i.e 'children' ) which in React can be used by every component to inject some content between the body tags. 'RootLayout' react component renders an HTML and body tag (this is to set up HTML skeleton of the website). the 'head' tag element is placed in the 'metadata' variable. 'metadata' variable is also reserved name. 'RootLayout' isn't a reserved name. Here 'metadata' variable can have title, description and other metadata fields which is applied to all pages that are covered by the layout here inside 'app/layout.js'. All the content given in 'head' tag is set to 'metadata' variable. 'children' ( mentioned in 'app/layout.js' as props to  'RootLayout' component) denotes to the content of page that's currently active (because 'app/layout.js' is a wrapper around app/page.js or one or more pages and depending on which path you are children will be content of the page.js that's currently active). layout.js is the wrapper and page.js is the actual content that will be injected as 'children' props in the 'layout.js'.

Other reserved filenames:-

globals.css - some CSS styles and this file is imported into 'app/layout.js' and this 'globals.css' is available on every page that's being loaded.
icon.png - if we give a file named 'icon.png' in app then this image given as 'icon.png' will be set as image icon in the tab in browser. Because 'icon.png' given as favicon which is the icon to tab.

In 'app' folder we add folders to provide the routes.
If we want to add a new component inside another component say 'header.js'. ' 'header.js' can be included in 'app/page.js' by adding the 'header.js' inside a folder named 'components' (and the 'components' folder placed in the root next to 'app' folder) .

components/header.js

export default function Header(){
return 
<>
<img src="/logo.png" alt = "A logo" />
</>
}



app/page.js

import Link from 'next/link';
import Header from '../components/header.js';

export default function Home() {
  return (
    <main>
      <Header />  
      <p><Link to="/about>About Us</Link></p>  
   </main>
  );
}






If we want to add 'blog' folder inside app as route and inside blog route there should be post-1, post-2 so on. If 'app/blog' should be a route it should have individual page.js file (i.e blog/page.js). But there is a problem here there can be multiple posts inside 'blog' route which we don't know (which depends on dynamic data from the database like post-1, post-2 and so on). To overcome this problem we use dynamic route (i.e we define route once but is capable of rendering different pages for different blog posts). To create dynamic route we place an identifier/placeholder (name of any choice) enclosed in square bracket (example:- [slug]  ) . Like 'app/blog/[slug]'. the identifier or placeholder (here 'slug' ) and inside 'app/blog/[slug]' we need a file 'page.js' (like:-  app/blog/[slug]/page.js  ). Where this 'page.js' file will provide content to the dynamic route pages (here slug). There also a page.js file inside 'app/blog' folder (i.e app/blog/page.js  ).



 app/blog/page.js


import Link from 'next/link';

export default function BlogPage() {
  return (
<main>
 <h1>Blog</h1>
 <p>
  <Link href="/blog/post-1">Post 1 </Link>
 </p>
<p>
  <Link href="/blog/post-2">Post 2 </Link>
 </p>
</main>
);
}



 app/blog/[slug]/page.js


export default function BlogPostPage({ params }) {
  return (
<main>
 <h1>Blog Post</h1>
{params.slug}
</main>
);
}


When we type this in  URL 'http://localhost:3000/blog' (the file component 'BlogPage' is loaded) where you will get to Links To Post 1 and Post 2. On clicking on any of these links 'Post 1' or 'Post 2' the content in the file ' app/blog/[slug]/page.js' comes that's with a header named 'Blog Post' (where 'BlogPostPage' component is loaded). But the URL changes to 'http://localhost:3000/blog/post-1' if 'Post-1' link is clicked and the URL changes to 'http://localhost:3000/blog/post-2' if 'Post-2' link is clicked. '[slug]' (i.e placeholder enclosed in square bracket) denotes that after 'http://localhost:3000/blog' we need a dynamic route say 'post-1' or 'post-2' or so on which we don't know since the route is dynamic. Here 'slug' which is the placeholder/identifier which give access to concrete value that we get when route is loaded.
Here in 'BlogPostPage' gets a props called 'params' (which is set by Nextjs) , 'params' are not set manually since we don't have to pass it manually the 'BlogPostPage', instead Nextjs are setting up the props in 'BlogPostPage' (i.e params). 'params' is an object which comprises of placeholder (here 'slug' ) had in dynamic route will be a key and value stored under key will be a concrete value encoded in the URL (here in 'http://localhost:3000/blog/post-1') the value will be 'post-1'). '{params.slug}' (where slug is the placeholder and params is the props we pass in dynamic route page.js file i.e in 'BlogPostPage' component) will give value 'post-1' if we are in the URL 'http://localhost:3000/blog/post-1'. This '{params.slug}' helps to extract value from database value for 'post-1' here for the link 'http://localhost:3000/blog/post-1' from  '{params.slug}' and place the content for post-1 in the page.






for 'http://localhost:3000/meals' we place 'app/meals' that has content in app/meals/page.js which is following

app/meals/page.js

export default function MealsPage() {
  return (
    <>
      <h1>Meals Page</h1>
    </>
)
}


for 'http://localhost:3000/meals/share' we place 'app/meals/share' that has content in app/meals/share/page.js which is following 


app/meals/share/page.js

export default function ShareMealsPage() {
  return (
    <>
      <h1>Meals Share Page</h1>
    </>
)
}



In 'app/community' for 'http://localhost:3000/community'


app/community/page.js


export default function CommunityPage() {
  return (
    <>
      <h1>Community Page</h1>
    </>
)
}





app/page.js

import Link from 'next/link';


export default function Home() {
  return (
    <main>
      <Header />  
      <p><Link href="/community>Join community</Link></p> 
      <p><Link href="/meals/share>Share meal</Link></p>  
      <p><Link href="/meals>Explore meals</Link></p> 
   </main>
  );
}



For dynamic route for 'http://localhost:3000/meals/<anything>  'app/meals/[mealsSlug]' 


app/meals/[mealsSlug]/page.js



export default function MealsDetailsPage() {
  return (
    <>
      <h1>Meals Details Page</h1>
    </>
)
}




To add a proper header, logo and navigation to this website we can provide in root layout.js (i.e app/layout.js ). Nested layouts can also be provided (for example if there is 'layout.js' inside 'app/meals/layout.js' this layout will be active for meals related pages, but this 'app/meals/layout.js' file be nested into the root layout.

app/meals/layout.js

export default function MealsLayout({children}) {
  return (
    <>
      <p>MealsLayout</p>
     {children}
    </>
)
}


Here when we give like below

<MealsLayout>This content</MealsLayout>

'This content' will be made available through the 'children' props in 'MealsLayout'. 'children' props in 'MealsLayout' will receive any nested layouts or pages.



