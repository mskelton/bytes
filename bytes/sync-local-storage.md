---
title: Sync localStorage Between Tabs
date: 2023-09-12
tags: [js, react]
---

Using `localStorage` is great for storing simple user preferences such as the
expanded/collapsed state of a sidebar, or the light/dark theme preference for
the site. An often overlooked but useful feature of `localStorage` is the
ability to sync changes between open tabs.

In the code snippet below, we create a simple `useLocalStorage` hook which is a
wrapper around `useState` to load the initial value from `localStorage` and
store changes to the value back into `localStorage`.

The magic comes in when we utilize `window.addEventListener("storage")` to
listen for changes to `localStorage` from other tabs on the same domain. When
another tab changes `localStorage`, we'll receive an event which we can use to
update the state in the current tab. Now if we have two open tabs and toggle the
website theme to dark mode, both tabs will become dark. No need to refresh!

This feels quite magical as a user and it's incredibly simple to implement!

```typescript
function useLocalStorage<T>(key: string, initialValue: T) {
  const [value, setValue] = useState<T>(() => {
    const json = localStorage.getItem(key)
    return json ? JSON.parse(json) : initialValue
  })

  useEffect(() => {
    function handleStorageChange(event: StorageEvent) {
      if (event.key === key) {
        setValue(e.newValue ? JSON.parse(e.newValue) : initialValue)
      }
    }

    window.addEventListener("storage", handleStorageChange)
    return () => window.removeEventListener("storage", handleStorageChange)
  }, [initialValue, key])

  const setValueAndStore = useCallback(
    (value: T) => {
      window.localStorage.setItem(key, JSON.stringify(value))
      setValue(value)
    },
    [key],
  )

  return [value, setValueAndStore] as const
}
```
