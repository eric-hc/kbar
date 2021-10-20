## kbar

kbar is a simple plug-n-play React component to add a fast, portable, and extensible <kbd>command</kbd> + <kbd>k</kbd> interface to your site.

![demo](https://user-images.githubusercontent.com/12195101/134022553-af4a29e9-0a3d-40f1-9254-3bd9673f3401.gif)

### Background

<kbd>Command</kbd> + <kbd>k</kbd> interfaces are used to create a web experience where any type of action users would be able to do via clicking can be done through a command menu.

With macOS's Spotlight and Linear's <kbd>command</kbd> + <kbd>k</kbd> experience in mind, kbar aims to be a simple 
abstraction to add a fast and extensible <kbd>command</kbd> + <kbd>k</kbd> menu to your site.

### Features

- Built in animations and fully customizable components
- Keyboard navigation support; e.g. <kbd>control</kbd> + <kbd>n</kbd> or <kbd>control</kbd> + <kbd>p</kbd> for the navigation wizards
- Keyboard shortcuts support for registering keystrokes to specific actions; e.g. hit <kbd>t</kbd> for Twitter
- Nested actions enable creation of rich navigation experiences; e.g. hit backspace to navigate to
  the previous action
- A simple data structure which enables anyone to easily build their own custom components

### Usage
Have a fully functioning command menu for your site in minutes. First, install kbar.

```
npm install kbar
```

At the root of your site, import and wrap the site with a KBarProvider.

```tsx
// app.tsx
import { KBarProvider } from "kbar";

return (
  <KBarProvider>
    <App />
  </KBarProvider>
);
```

kbar is built on top of `actions`. Actions define what to execute when a user selects it. Actions can have children which are just other actions.

We'll create a few static actions first. Static actions are actions with no external dependencies. Our example below sets the `window.location.pathname`, which does not rely on any
external hook, for instance.

```tsx
const actions = [
  {
    id: "blog",
    name: "Blog",
    shortcut: ["b"],
    keywords: "writing words",
    perform: () => (window.location.pathname = "blog"),
  },
  {
    id: "contact",
    name: "Contact",
    shortcut: ["c"],
    keywords: "email",
    perform: () => (window.location.pathname = "contact"),
  },
];

return (
  <KBarProvider actions={actions}>
    <App />
  </KBarProvider>
);
```

kbar exposes a few components which handle animations, keyboard events, default styles, etc. You can use them together like so:

```tsx
import { 
  KBarProvider, 
  KBarPortal, 
  KBarPositioner, 
  KBarAnimator, 
  KBarSearch, 
  KBarResults 
} from "kbar";

<KBarProvider actions={actions}>
  <KBarPortal> // Renders the content outside the root node
    <KBarPositioner> // Centers the content
      <KBarAnimator> // Handles the show/hide and height animations
        <KBarSearch /> // Search input
        <KBarResults /> // Results renderer
      </KBarAnimator>
    </KBarPositioner>
  </KBarPortal>
  <MyApp />
</KBarProvider>;
```

Hit <kbd>cmd</kbd>+<kbd>k</kbd> (or <kbd>ctrl</kbd>+<kbd>k</kbd>) and you should see a primitive command menu. kbar allows you to have full control over all
aspects of your command menu – refer to the <a href="https://kbar.vercel.app/docs">docs</a> to get
an understanding of further capabilities. Excited to see what you build.

### Contributing to kbar

Contributions are welcome!

#### New features

Please [open a new issue](https://github.com/timc1/kbar/issues) so we can discuss prior to moving
forward.

#### Bug fixes

Please [open a new Pull Request](https://github.com/timc1/kbar/pulls) for the given bug fix.

#### Nits and spelling mistakes

Please [open a new issue](https://github.com/timc1/kbar/issues) for things like spelling mistakes
and README tweaks – we will group the issues together and tackle them as a group. Please do not
create a PR for it!
