# WINDOW
```javascript
componentDidMount() {
  window.addEventListener('scroll', () => {
    if (window.innerHeight + window.scrollY >= document.body.offsetHeight) {
      // update
    }
  });
}
```

![Window Scroll](../img/window-scroll.png)

# ELEMENT
```javascript
componentDidMount() {
  this.refs.iScroll.addEventListener("scroll", () => {
    if (this.refs.iScroll.scrollTop + this.refs.iScroll.clientHeight >= this.refs.iScroll.scrollHeight) {
      // update
    }
  });
}

render() {
  return (
    <div ref="iScroll" style={{ height: "200px", overflow: "auto" }} />
  );
}
```

![Elem Scroll](../img/elem-scroll.png)
