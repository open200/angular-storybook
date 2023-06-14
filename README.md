# Storybook Setup

To install Storybook, perform the following steps inside your angular application:

1. In the root directory of your project, run the command npx storybook@latest init.
2. During the setup process, choose "no" to ignore the creation of compodoc.
3. This command will generate a `.storybook` folder and a `stories` folder.
   - The .storybook folder contains the configuration for Storybook.
   - The stories folder contains the component stories.

Storybook is a development environment for UI components that allows you to:
   - Browse a component library
   - View different states of each component
   - Interactively develop and test components

The build-storybook command is used to build the Storybook as a static web application, which can be deployed later.

# Storybook Configuration

To configure Storybook, follow these steps:

1. Remove the .stories folder, as it is recommended to build the Storybook files inside the src folder of your project. This simplifies deployment to GitHub Pages.
2. Open the `angular.json` file in the `root` folder and modify the "storybook" and "build-storybook" configurations as shown below:

```
"storybook": {
          "builder": "@storybook/angular:start-storybook",
          "options": {
            "configDir": ".storybook",
            "browserTarget": "angular-storybook:build",
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ],
            "compodoc": false,
            "port": 6006
          }
        },
        "build-storybook": {
          "builder": "@storybook/angular:build-storybook",
          "options": {
            "configDir": ".storybook",
            "browserTarget": "angular-storybook:build",
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ],
            "compodoc": false,
            "outputDir": "public"
          }
        }
      } 
```
Explanation of the modifications:
1. Added the `assets` part to the `storybook` and `build-storybook` configuration to allow using assets in Storybook.
2. If you plan to deploy to GitLab/GitHub Pages, rename the output directory of `build-storybook` to `public`.
3. Before compiling, remove the `.angular` and `storybook-static` folders by running the command `rm -rf .angular storybook-static`. 
4. If the build is not functioning properly, run the command `npm run build-storybook`


# Creating Button Component

1. Create an Angular component named `Button` by running the command `ng generate component button` in the `components` folder and customize it to meet your requirements.
2. Create a file named `button.stories.ts` in the same folder as the `Button` component and paste the following code:
typescript

```import type { Meta, StoryObj } from '@storybook/angular';
import { ButtonComponent } from './button.component';

// More on how to set up stories at: https://storybook.js.org/docs/angular/writing-stories/introduction
const meta: Meta<ButtonComponent> = {
  component: ButtonComponent,
  tags: ['autodocs'],
};

export default meta;
type Story = StoryObj<ButtonComponent>;

// More on writing stories with args: https://storybook.js.org/docs/angular/writing-stories/args
export const Primary: Story = {
  args: {
    buttonText: 'open200 Software Company',
  },
};
```

# Running Storybook

1. Run `npm run build-storybook` to build the Storybook.
2. Run `npm run storybook` to start the Storybook development server and view your components in the browser.
