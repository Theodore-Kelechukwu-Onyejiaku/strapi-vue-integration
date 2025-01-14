## What is Strapi?
Strapi is the leading open-source headless CMS offering [features](https://strapi.io/features), like customizable APIs, role-based permissions, multilingual support, etc. It simplifies content management and integrates effortlessly with modern [frontend frameworks](https://strapi.io/blog/comprehensive-review-of-top-javascript-frontend-frameworks).

Explore the [Strapi documentation](https://docs.strapi.io/) for more details.


## What is Vue.js?
[Vue.js](https://vuejs.org/) is a JavaScript framework for building user interfaces. It builds on top of standard HTML, CSS, and JavaScript and provides a declarative, component-based programming model that helps you efficiently develop user interfaces of any complexity.

Visit the [Vue.js documentation](https://vuejs.org/guide/introduction.html) for more.

## Strapi and Vue.js Integration

The out-of-the-box Strapi features allow you to get up and running in no time:
1. **Single types**: Create one-off pages that have a unique content structure
2. **Customizable API**: With Strapi, you can just hop in your code editor and edit the code to fit your API to your needs.
3. **Integrations**: Strapi supports integrations with Cloudinary, SendGrid, Algolia, and others.
4. **Editor interface**: The editor allows you to pull in dynamic blocks of content.
5. **Authentication**: Secure and authorize access to your API with JWT or providers.
6. **RBAC**: Help maximize operational efficiency, reduce dev team support work, and safeguard against unauthorized access or configuration modifications.
7. **i18n**: Manage content in multiple languages. Easily query the different locales through the API.

Learn more about [Strapi features](https://strapi.io/features).

## Setup Strapi 5 Headless CMS

We are going to start by setting up our Strapi 5 project with the following command:

> 🖐️ Note: make sure that you have created a new directory for your project.

You can find the full documentation for Strapi 5 [here](https://docs.strapi.io/dev-docs/intro).

``` bash
npx create-strapi-app@latest server
```

You will be asked to choose if you would like to use Strapi Cloud we will choose to skip for now.

``` bash
 Strapi   v5.6.0 🚀 Let's create your new project

 
We can't find any auth credentials in your Strapi config.

Create a free account on Strapi Cloud and benefit from:

- ✦ Blazing-fast ✦ deployment for your projects
- ✦ Exclusive ✦ access to resources to make your project successful
- An ✦ Awesome ✦ community and full enjoyment of Strapi's ecosystem

Start your 14-day free trial now!


? Please log in or sign up. 
  Login/Sign up 
❯ Skip 
```

After that, you will be asked how you would like to set up your project. We will choose the following options:

``` bash
? Do you want to use the default database (sqlite) ? Yes
? Start with an example structure & data? Yes <-- make sure you say yes 
? Start with Typescript? Yes
? Install dependencies with npm? Yes
? Initialize a git repository? Yes
```

Once everything is set up and all the dependencies are installed, you can start your Strapi server with the following command:

``` bash
cd server
npm run develop
```

You will be greeted with the **Admin Create Account** screen.

![003-strapi-5.png](https://delicate-dawn-ac25646e6d.media.strapiapp.com/003_strapi_5_0ec1eaaa6a.png)

Go ahead and create your first Strapi user.  All of this is local so you can use whatever you want.

Once you have created your user, you will be redirected to the **Strapi Dashboard** screen.

![004-strapi-5.png](https://delicate-dawn-ac25646e6d.media.strapiapp.com/004_strapi_5_87bc6d8f39.png)

### Publish Article Entries
Since we created our app with the example data, you should be able to navigate to your **Article** collection and see the data that was created for us.

![005-strapi-5.png](https://delicate-dawn-ac25646e6d.media.strapiapp.com/005_strapi_5_dc3a4a7540.png)

Now, let's make sure that all of the data is **published**.  If not, you can select all items via the checkbox and then click the **Publish** button.

![Strapi Articles Published](https://delicate-dawn-ac25646e6d.media.strapiapp.com/006_strapi_5_9c6055ac59.png)

### Enable API Access
Once all your articles are published, we will expose our Strapi API for the **Articles Collection**. This can be done in ***Settings -> Users & Permissions plugin -> Roles -> Public -> Article***.

You should have `find` and `findOne` selected.  If not, go ahead and select them.

![007-strapi-5.png](https://delicate-dawn-ac25646e6d.media.strapiapp.com/007_strapi_5_edd775db5f.png)

### Test API 
Now, if we make a `GET` request to `http://localhost:1337/api/articles`, we should see the following data for our articles.

![008-strapi-5.png](https://delicate-dawn-ac25646e6d.media.strapiapp.com/008_strapi_5_66883c2963.png)

> 🖐️ Note: that article covers (images) are not returned. This is because the REST API by default does not populate any relations, media fields, components, or dynamic zones.. Learn more about [REST API: Population & Field Selection](https://docs.strapi.io/dev-docs/api/rest/populate-select).


So let's get the article covers by using the `populate=*` parameter: `http://localhost:1337/api/articles?populate=*`

![vuejs strapi integration - api request.png](https://delicate-dawn-ac25646e6d.media.strapiapp.com/vuejs_strapi_integration_api_request_c748d16c83.png)



Nice, now that we have our Strapi 5 server setup, we can start to setup our Vue.js application.

## Create a Vue.js app

Create a basic Vue.js application using the command below. This command will install and execute `create-vue`, the official Vue project scaffolding tool.

```bash
npm create vue@latest
```

After running the command above, you will prompted with the following. Your answers will depend on your preferred setup.

```bash
✔ Project name: … vue-project
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit Testing? … No / Yes
✔ Add an End-to-End Testing Solution? › No
✔ Add ESLint for code quality? › No
```

Once your project is created, run the command below to install dependencies and start the dev server:

```bash
cd <your-project-name>
npm install
npm run dev
```

You should now have your first Vue project running on "http://localhost:5173" as shown below:

![New Vue.js Project](https://delicate-dawn-ac25646e6d.media.strapiapp.com/New_Vue_js_Project_72bb8a47e3.png)



## Add Tailwind CSS To Vue.js Project
We will install [Tailwind CSS](https://tailwindcss.com/) as a PostCSS plugin. This is the most seamless way.

### Install Tailwind
Run the command below:
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init
```
The command above will create a Tailwind CSS configuration file called `tailwind.config.js`.

### Add Tailwind CSS to your PostCSS configuration
Create a configuration file called `postcss.config.cjs` at the root of your project and add the following code:


```javascript
// Path: ./postcss.config.cjs

module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  }
}
```
### Add Template Paths
Add the paths to all of your template files:

```javascript
// Path: ./tailwind.config.js

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ['./index.html', './src/**/*.{vue,js,ts,jsx,tsx}'],
  theme: {
    extend: {
    },
  },
  plugins: [],
}
```

### Add the Tailwind directives to your CSS
Inside the `./src/assets/main.css` file, replace the code with the following code:

```css
/** Path: ./src/assets/main.css **/

@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Restart Vue.js Application
After Tailwind CSS setup, ensure you restart your application.

```bash
npm run dev
```

## Use an HTTP Client For Requests
Many HTTP clients are available, but on this integration page, we'll use [Axios](https://github.com/axios/axios) and [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).

### Using Axios
Install Axios by running any of the commands below:

```bash
# npm
npm i axios

# yarn
yarn add axios
```

### Using fetch
No installation needed

## GET Request Your Collection type
Execute a `GET` request on the **Article** collection type in order to fetch all your articles.

Be sure that you activated the `find` permission for the `Article` collection type.

> 🖐️ NOTE: We want to also fetch covers (images) of articles, so we have to use the `populate` parameter as seen below.

### Using Axios
```javascript
import axios;

// fetch articles along with their covers
const response = await axios.get("http://localhost:1337/api/articles?populate=*");
console.log(response.data.data);
```

### Using Fetch
```javascript
const response = await fetch("http://localhost:1337/api/articles?populate=*");
const data = await response.json();
console.log(data.data);
```

## Example Code
Inside the `./src/App.vue`, we will be using the Composition API. Check out [Vue.js API styles](https://vuejs.org/guide/introduction.html#api-styles) to learn more.

### Set Up The Script Section
Add the following to the `<script setup>` section:

```javascript
// Path: ./src/App.vue

<script setup>
// Import dependencies
import { ref, onMounted } from "vue";

// Variables
const articles = ref([]);

// Strapi Base URL
const STRAPI_URL = "http://localhost:1337" || import.meta.env.VITE_STRAPI_URL;

// Fetch articles
const getArticles = async () => {
  const response = await fetch(`${STRAPI_URL}/api/articles?populate=*`);
  const data = await response.json();
  articles.value = data.data;
};

// Format date
const formatDate = (date) => {
  const options = { year: "numeric", month: "2-digit", day: "2-digit" };
  return new Date(date).toLocaleDateString("en-US", options);
};

// Fetch articles on component mount
onMounted(() => {
  getArticles();
});
</script>
```

Here is what we did above:
* The `ref` and `onMounted` are imported from Vue for managing reactive state and lifecycle hooks, respectively.
* `articles` reactive variable initialized as an empty array. This will store the articles fetched from the Strapi API.
* `STRAPI_URL` Defines the base URL for the Strapi API. It falls back to "http://localhost:1337" by default but allows for environment configuration using `import.meta.env.VITE_STRAPI_URL`.
* `getArtices`: An asynchronous function that fetches articles from Strapi. It sends a request to the Strapi API's `/api/articles?populate=*` endpoint, which retrieves all articles along with their associated media (images). The response is parsed into JSON, and the article data is assigned to the `articles` reactive variable.
* `formatDate` function formats the `publishedAt` date of each article into a human-readable string (e.g., 01/14/2025). It uses the `toLocaleDateString` method with options to display the year, month, and day in a `MM/DD/YYYY` format.
* The `onMounted` hook ensures that the `getArticles` function is called once the component is mounted to the DOM. This is when the data is fetched from Strapi.

### Display Articles in The Template Section: `<template>`
This section defines the structure and layout of the UI, utilizing Tailwind CSS classes for styling.

```javascript
// Path: ./src/App.vue

<template>
  <div class="p-6">
    <h1 class="text-4xl font-bold mb-8">Vue.js and Strapi Integration</h1>
    <div>
      <h2 class="text-2xl font-semibold mb-6">Articles</h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <article
          v-for="article in articles"
          :key="article.id"
          class="bg-white shadow-md rounded-lg overflow-hidden"
        >
          <img
            :src="STRAPI_URL + article.cover.url"
            alt="Article Image"
            class="w-full h-48 object-cover"
          />
          <div class="p-4">
            <h3 class="text-lg font-bold mb-2">{{ article.title }}</h3>
            <p class="text-gray-600 mb-4">{{ article.content }}</p>
            <p class="text-sm text-gray-500">
              Published: {{ formatDate(article.publishedAt) }}
            </p>
          </div>
        </article>
      </div>
    </div>
  </div>
</template>
```

Now, this is what your Vue.js project should look like:

![Vuejs and Strapi Example project.png](https://delicate-dawn-ac25646e6d.media.strapiapp.com/Vuejs_and_Strapi_Example_project_d276b3154b.png)


Awesome, great job!

## Github Project Repo
You can find the complete code for this project in the following [Github repo](https://github.com/Theodore-Kelechukwu-Onyejiaku/strapi-vue-integration).


## Strapi Open Office Hours
If you have any questions about Strapi 5 or just would like to stop by and say hi, you can join us at **Strapi's Discord Open Office Hours** Monday through Friday at 12:30 pm - 1:30 pm CST: [Strapi Discord Open Office Hours](https://discord.com/invite/strapi)

For more details, visit the [Strapi documentation](https://strapi.io/documentation) and [Astro documentation](https://docs.astro.build/en/getting-started).