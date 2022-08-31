---
title: React function component in TypeScript
description: Showing simple example of React using TypeScript.
date: 2021-05-15
layout: layouts/post.njk
tags: [react, typescript]
---

For the past couple of months I've been learning TypeScript and using it in a
NextJS app.

At first it was a little daunting, but I've come to enjoy using the simple
features it gives around types.

Here's what a typical function component may look like this:

```jsx
import React, { useState } from "react";
import PropTypes from "prop-types";

const Component = ({ darkMode, title, advancedMode }) => {
  const [name, setName] = useState("");
  const [isHuman, setIsHuman] = useState(false);

  return <div></div>;
};

Component.propTypes = {
  darkMode: PropTypes.bool,
  title: PropTypes.string,
  advancedMode: PropTypes.bool,
};

export default Component;
```

Here's what the TypeScript version of the above component looks like:

```tsx
import React, { FC, useState } from "react";

interface Props {
  darkMode: boolean;
  title: string;
  advancedMode?: boolean;
}

const Component: FC<Props> = ({ darkMode, title, advancedMode }) => {
  const [name, setName] = useState<string>("");
  const [isHuman, setIsHuman] = useState<boolean>(false);

  return <div></div>;
};

export default Component;
```
