## Questions on Web Storage APIs 

###### How long is cool_secret accessible?

```js
sessionStorage.setItem('cool_secret', 123);
```

- A: Forever, the data doesn't get lost.
- B: When the user closes the tab.
- C: When the user closes the entire browser, not only the tab.
- D: When the user shuts off their computer.

**Answer**:

Answer: B

The data stored in `sessionStorage` is removed after closing the *tab*.

If you used `localStorage`, the data would've been there forever, unless for example `localStorage.clear()` is invoked.