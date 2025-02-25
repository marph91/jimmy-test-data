You can use ref callbacks to measure the rendered size of React components, did you know? It's a neat little trick.
<https://codesandbox.io/embed/71vx2q5r76>
Here's how it works 👇
1. React renders your component
2. Browser layout engine does its thing
3. ref callback fires
4. Use `getBoundingClientRect` to measure element size
5. Use this info for whatever you want
We used this trick in this [Dynamic SVG accordion example](https://swizec.com/blog/build-animated-accordion-react-d3/swizec/8418) and in this [Tiny React & D3 flamegraph tutorial](https://swizec.com/blog/tiny-react-d3-flamegraph-tutorial/swizec/8440). That's because layouting in SVG is hard, and you have to do everything yourself.
Using ref callbacks to measure your elements is a little less useful in the modern HTML + CSS world. You can use flexbox and css-grid so you never need to know what you're dealing with.
And yet when push comes to shove, sometimes you just really need your code to know the size of an element.
A minimal size reporting component looks like this 👇

```
class ReportSize extends React.Component {
  refCallback = element => {
    if (element) {
      this.props.getSize(element.getBoundingClientRect());
    }
  };

  render() {
    return (
      
        {faker.lorem.paragraphs(Math.random() * 10)}
      
    );
  }
}
```

The `render` method outputs a `<div>` with a ref callback and a red border. Inside, we use `faker` to generate up to 10 random paragraphs.
After React places this element, it calls `refCallback` with a reference to the rendered DOM node. We can then use [`getBoundingClientRect`](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect) to measure its size.

```
{
  "x": 8,
  "y": 158.8125,
  "width": 544,
  "height": 340,
  "top": 158.8125,
  "right": 552,
  "bottom": 498.8125,
  "left": 8
}
```

All sorts of useful info!

## So why not just use `componentDidMount`?

Yes, that works too. But it's less elegant because you have to save the `ref` first. The `refCallback` API calls your function with a nice reference already packaged in.
However, you might still have to do that if your component size changes *after* initial render. Observe 👇
<https://codesandbox.io/embed/v6m4o48zl>
Clicking the `shuffle` button doesn't report new sizing information up the hierarchy. That's not good 🤔
If your component changes size without re-mounting, you have to re-measure its size in `componentDidUpdate` as well. But that way lies trouble… you can fall into the infinite recursion trap.
You can solve the problem with a lock, like this 👇
<https://codesandbox.io/embed/7jqmo1jn8j>
Keep clicking `shuffle` and sizing info is always correct.
The key is enabling size reporting when you logically know size is going to change, in `shuffle`, and disabling it as soon as you report the change in `componentDidUpdate`.

```
shuffle = () => {
    this.doReportSize = true;
    this.setState({
      text: faker.lorem.paragraphs(Math.random() * 10)
    });
  };

  refCallback = element => {
    if (element) {
      this.elementRef = element;
      this.props.getSize(element.getBoundingClientRect());
    }
  };

  componentDidUpdate() {
    if (this.doReportSize) {
      this.props.getSize(this.elementRef.getBoundingClientRect());
      this.doReportSize = false;
    }
  }
```

Oof, not pretty. Setting a `this.elementRef` in our callback, messing around with class properties for flags. Pretty sure we could've just used the new `React.createRef()` API in combination with `componentDidMount` and `componentDidUpdate`.
Would still need the flag to prevent infinite loops, however.
I wonder if using class properties to make render flags like that will continue to work when asynchronous rendering comes with React 17 🤔