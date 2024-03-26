## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

# Responsive Navigation

## Overview

I was tasked to build a navigation compoennt that is fully responsive and matches the supplied Figma designs, using Vue3.

## Technical Requirements

1. Desktop:
   ⁃ Rolling over ‘Platform’ displays the dropdown menu
   ⁃ Rolling over each of the platform features (Feedback & Sentiment Analysis etc. which should change the content of the dropdown for that section).

2. Mobile:
   ⁃ Tap the burger menu to display the menu
   ⁃ Tap the ‘Platform’ section to expand the accordion
   ⁃ Tap the different platform features (Feedback & Sentiment Analysis etc) to display the relevant section content.

## Technologies Used

- Vite (Vue)
- HTML
- CSS (SASS)
- Bootstrap for responsive break points and css reboot
- JSON
- NPM
- Node v20.11.1 (npm v10.2.4)

## Approach

1. Initialise the Vue project on a develop branch (Git). VueCLI is currently in maintenance mode (as stated in their documentation) therefore I created the project using Vite, with Prettier and Lint preinstalled to kick start the project.
2. I set up the project files and structure, created a Navigation component and CSS folders using an atomic approach. This folder consisted of generic styles and variables for colors, typography, mixins etc.
3. Installed SASS and Bootstrap (using Bootstrap for responsive media queries and css reboot).
4. Next I began to create the Navigation component, with a mobile first approach. Starting with the logo and toggle controls to show/hide the primary menu (Platform, Resources, About, Login).
5. Created a JSON file containing Navigation data which mimics data from an API response.
6. Following the Vue features, I iterated through the data to create the collpsable secondary menu and its data.
7. Moving onto the Desktop view, I added 'Platform Capabilities' and the 'Article' section to display in the mega menu. Added responsive styles to the desktop to match the design.

## Challenges and improvements

- Time spent roughly to build the navigation was a days work (8 hours).
- Update the desktop view to display the sub menu on hover rather than on click.
- Position the 'Login' button to the end of the Nav rather than centered.
- Tidy up the styling, I didn't have Dev mode in Figma so I tried my best to match the spacing as accurately as possible (by adding rectangles between elements to measure the exact spacing)
- Use Fetch request to pull the data from the JSON file to minic a live build. Currently the file is imported directly into the Navigation component.
- Update the component on Desktop using visibility and opacity to make for a smoother dropdown (rather than display: block / hide).
- Fix the overflow bug when the menu is open on Mobile
- Create a Button.vue element with dynamic values for reusability.
- Update aria accessibility tags when user interacts with the Navigation.
