# example

### state.js
```js
import { readable, writable } from 'ryucheat-state-react';

export const name = writable('ryujaewan');

export const date = readable(new Date(), (set) => {
    let interval = setInterval(() => {
        set(new Date());
    }, 1000);

    return () => clearInterval(interval);
});
```


### index.js
```js
import { name, date } from './state';
import { unmount } from 'ryucheat-state-react';

class CustomView1 extends React.Component {
  componentWillUnmount() {
    unmount(this);
  }
  render() {
    let d = date(this);
    return <>
      <Text>{d.toLocaleString()}</Text>
    </>
  }
}

class CustomView2 extends React.Component {
  componentWillUnmount() {
    unmount(this);
  }
  render() {
    let n = name(this);
    return <Text>{name}</Text>
  }
}

export default class APP extends React.Component {
  render() {
    return (<>
      <CustomView1 />
      <CustomView2 />
    </>);
  }
}
```

### update
```js
name.set('ryucheat')
```
use the `.set()`, all components referencing this state will be updated.


### readable(value, initiator), writable(value, initiator)
```js
export const date = readable(new Date(), (set) => {
    let interval = setInterval(() => {
        set(new Date());
    }, 1000);

    return () => clearInterval(interval);
});
```
The above code updates date once every second.  
And when all components are unmounted, the returned function will be executed.  
