- [jasnell web streams in node](https://www.jasnell.me/posts/webstreams)
```js
import { ReadableStream, WritableStream } from 'node:stream/web';

function getSomeSource() {
  let count = 0;
  const  maxCount = 5;
  return {
    start(controller) {
      // This is called when the readable stream is constructed
    },
    pull(controller) {
      // This is called when the consumer wants to read data
      
      if(count < maxCount) {
        controller.enqueue(`some data; count: ${count}`);
        count++;
      } else {
        controller.close();
      }
    },
    cancel(reason) {
      // This is called when the consumer cancels the stream
    }
  };
}

function getSomeSink() {
  return {
    start(controller) {
      // This is called when the writable stream is constructed
    },
    write(chunk, controller) {
      // This is called when the consumer writes data
      console.log(chunk);
    },
    close(controller) {
      // This is called when the consumer closes the stream
    },
    abort(reason) {
      // This is called when the consumer aborts the stream
    }
  };
}

(async () => {
  
  const readable = new ReadableStream(getSomeSource());
  const writable = new WritableStream(getSomeSink());
  
  await readable.pipeTo(writable);
})();


// import {
//   ReadableStream,
//   WritableStream
// } from 'node:stream/web';

// const readable = new ReadableStream(getSomeSource());
// const writable = new WritableStream(getSomeSink());

// await readable.pipeTo(writable);

```



