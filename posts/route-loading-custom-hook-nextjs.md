---
title: Detect when the page/route is loading with custom hook - NextJS
description: A simple custom hook that will allow you to detect when your page/route is in a loading state.
date: 2021-05-26
layout: layouts/post.njk
tags: [NextJS, "Custom Hook"]
---

**Update 2021-09-28: NextJS have updated the recommended way to detect loading since version 11. The examples have been updated. Old example can be found at the <a href="#old-examples">bottom of the post</a>.**

Within NextJS's router there are events that can be captured using Router from
next/router.

Below is a simple custom hook that gives you a loading state boolean that you
can use anywhere within your NextJS project.

TypeScript

```tsx
import { useRouter } from "next/router";
import { useEffect } from "react";
import { useState } from "react";

const useLoading = (): boolean => {
  const [loading, setLoading] = useState<boolean>(false);
  const router = useRouter();

  useEffect(() => {
    const handleIsLoading = () => {
      setLoading(true);
    };

    const handleNotLoading = () => {
      setLoading(false);
    };

    router.events.on("routeChangeStart", handleIsLoading);
    router.events.on("routeChangeComplete", handleNotLoading);
    router.events.on("routeChangeError", handleNotLoading);

    return () => {
      router.events.off("routeChangeStart", handleIsLoading);
      router.events.off("routeChangeComplete", handleNotLoading);
      router.events.off("routeChangeError", handleNotLoading);
    };
  }, [router]);

  return loading;
};

export default useLoading;
```

JavaScript

```jsx
import { useRouter } from "next/router";
import { useEffect } from "react";
import { useState } from "react";

const useLoading = () => {
  const [loading, setLoading] = useState(false);
  const router = useRouter();

  useEffect(() => {
    const handleIsLoading = () => {
      setLoading(true);
    };

    const handleNotLoading = () => {
      setLoading(false);
    };

    router.events.on("routeChangeStart", handleIsLoading);
    router.events.on("routeChangeComplete", handleNotLoading);
    router.events.on("routeChangeError", handleNotLoading);

    return () => {
      router.events.off("routeChangeStart", handleIsLoading);
      router.events.off("routeChangeComplete", handleNotLoading);
      router.events.off("routeChangeError", handleNotLoading);
    };
  }, [router]);

  return loading;
};

export default useLoading;
```

---

## Old examples

TypeScript

```tsx
import { Router } from "next/router";
import { useState } from "react";

const useLoading = (): boolean => {
  const [loading, setLoading] = useState<boolean>(false);

  Router.events.on("routeChangeStart", () => {
    setLoading(true);
  });

  Router.events.on("routeChangeComplete", () => {
    setLoading(false);
  });

  Router.events.on("routeChangeError", () => {
    setLoading(false);
  });

  return loading;
};

export default useLoading;
```

JavaScript

```jsx
import { Router } from "next/router";
import { useState } from "react";

const useLoading = () => {
  const [loading, setLoading] = useState(false);

  Router.events.on("routeChangeStart", () => {
    setLoading(true);
  });

  Router.events.on("routeChangeComplete", () => {
    setLoading(false);
  });

  Router.events.on("routeChangeError", () => {
    setLoading(false);
  });

  return loading;
};

export default useLoading;
```
